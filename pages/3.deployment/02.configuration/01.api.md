---
layout: page
title: Api
permalink: /deployment/configuration/api
---

Tweek api service can be configured by setting environment variables or by mounting /app/appsettings.Production.json file.
In the json format, keys are configured as nested objects:
```
{
  "Rules": {
        "Management": {
            "Url": "http://management:3000"
        }
  },
}
```
The equivalent environment variable configuration is:
```
Rules__Management__Url=http://management:3000
```

### Context configuration
Tweek context provider is pluggable as an addon.  

For Redis provider, add the following configuration:
```
- Addons__Redis__ClassName=Tweek.Drivers.Redis.RedisServiceAddon
- Addons__Redis__AssemblyName=Tweek.Drivers.Redis
- Redis__ConnectionString=*******
```

For Couchbase provider add:
```
- Addons__Couchbase__ClassName=Tweek.Drivers.CouchbaseDriver.CouchBaseServiceAddon
- Addons__Couchbase__AssemblyName=Tweek.Drivers.Couchbase
- Couchbase__BucketName": "tweek-context"
- Couchbase__Password": "pass", #bucket password
- Couchbase__Url: "http://couchbase-url/"
```

### Monitoring
Tweek support [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) and [graphite](https://graphiteapp.org/) (through [AppMetrics](http://app-metrics.io/)) for monitoring providers.

To add Application Insights, add the following configuration:
```
- Addons__ApplicationInsights__ClassName=Tweek.Addons.ApplicationInsights.ApplicationInsightsAddon
- Addons__ApplicationInsights__AssemblyName=Tweek.Addons.ApplicationInsights
- ApplicationInsights__InstrumentationKey=*******
```
For Graphite, add:
```
- Addons__GraphiteReporter__ClassName=Tweek.Addons.AppMetrics.GraphiteReporter.GraphiteReporterAddon
- Addons__GraphiteReporter__AssemblyName=Tweek.Addons.AppMetrics.GraphiteReporter
- AppMetricsReporters__Graphite__Prefix=myprefix
- AppMetricsReporters__Graphite__Url=graphite.domain.com
```
Since Graphite reporter use AppMetrics, you can use  [AppMetrics configuration](http://app-metrics.io/getting-started/fundamentals/configuration.html) as well, for example: 
```
{
    "AppMetrics": {
        "DefaultContextLabel": "MyContext",
        "MetricsEnabled": true,
        "ReportingEnabled": true,
        "GlobalTags": { "env": "stage" }  
    }
}
```

### Security
TBD
