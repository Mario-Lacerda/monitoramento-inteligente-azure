# Desafio Dio - Monitoramento Inteligente com o Azure

####     Projeto ainda mais completo e abrangente com mais códigos para: Monitoramento Inteligente com o Azure



**Introdução**

Este projeto irá guiá-lo pelos fundamentos do monitoramento inteligente no Microsoft Azure, uma plataforma de computação em nuvem que oferece uma ampla gama de serviços para ajudá-lo a monitorar e analisar o desempenho e a disponibilidade de seus aplicativos e recursos de infraestrutura.



### **Pré-requisitos**

- Uma conta do Microsoft Azure

- O Visual Studio 2019 ou superior

- O .NET Core SDK 3.1 ou superior

  

### **Instruções**

1. **Crie um novo projeto do Visual Studio.**

2. **Selecione o modelo "Aplicativo Web do ASP.NET Core".**

3. **Nomeie o projeto como "AzureIntelligentMonitoringInAction".**

4. **Clique em "Criar".**

   

5. #### Adicione os seguintes pacotes NuGet ao projeto:

   

   - Microsoft.Azure.Management.Insights

   - Microsoft.Azure.Management.ResourceManager

     

6. #### Adicione as seguintes classes ao projeto:

   

   - **InsightsService.cs:** Esta classe fornece métodos para interagir com o serviço Insights do Azure.

   - **ResourceManagerService.cs:** Esta classe fornece métodos para interagir com o serviço Resource Manager do Azure.

     

7. #### **Adicione o seguinte código ao arquivo "Startup.cs":**

   

csharp



```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IInsightsService, InsightsService>();
    services.AddSingleton<IResourceManagerService, ResourceManagerService>();
}
```



1. **Adicione o seguinte código ao arquivo "Controllers/HomeController.cs":**

   

csharp



```csharp
public class HomeController : Controller
{
    private readonly IInsightsService _insightsService;
    private readonly IResourceManagerService _resourceManagerService;

    public HomeController(IInsightsService insightsService, IResourceManagerService resourceManagerService)
    {
        _insightsService = insightsService;
        _resourceManagerService = resourceManagerService;
    }

    public IActionResult Index()
    {
        return View();
    }

    [HttpPost]
    public async Task<IActionResult> GetMetricDefinitions(string resourceId)
    {
        var metricDefinitions = await _insightsService.GetMetricDefinitionsAsync(resourceId);

        return View("MetricDefinitions", metricDefinitions);
    }

    [HttpPost]
    public async Task<IActionResult> GetMetricData(string resourceId, string metricName, string startTime, string endTime)
    {
        var metricData = await _insightsService.GetMetricDataAsync(resourceId, metricName, startTime, endTime);

        return View("MetricData", metricData);
    }

    [HttpPost]
    public async Task<IActionResult> CreateAlertRule(string resourceId, string metricName, string condition, string action)
    {
        await _insightsService.CreateAlertRuleAsync(resourceId, metricName, condition, action);

        return RedirectToAction("Index");
    }

    [HttpPost]
    public async Task<IActionResult> ListAlertRules(string resourceId)
    {
        var alertRules = await _insightsService.ListAlertRulesAsync(resourceId);

        return View("AlertRules", alertRules);
    }
}
```



1. #### **Execute o projeto.**

   

## **Conclusão**



Este projeto fornece uma base ainda mais sólida para você começar a usar o monitoramento inteligente na nuvem no Microsoft Azure. Você pode usar o serviço Insights para obter definições de métricas, dados de métricas e criar regras de alerta para seus recursos, e usar o serviço Resource Manager para listar os recursos em seu escopo.


https://learn.microsoft.com/pt-br/azure/iot-central/energy/tutorial-solar-panel-app

https://learn.microsoft.com/pt-br/azure/iot-central/government/tutorial-water-quality-monitoring

https://learn.microsoft.com/pt-br/azure/azure-monitor/alerts/smart-detection-performance

https://learn.microsoft.com/pt-pt/azure/azure-sql/database/monitor-tune-overview?view=azuresql


  
