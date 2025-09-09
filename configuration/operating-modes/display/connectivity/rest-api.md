# REST API

The output of a display script can also be accessed via an HTTP GET call to `https://www.remoteredirect.com/api/links/{linkId}/output`

This can be useful when not feeding display boards with data but any other external software with HTTP capabilities.&#x20;

This is also very useful when connecting our ScreensPro videowall solution with RemoteRedirect. ScreensPro Server will constantly query the API for an updated start time and then display it in the layout accordingly.&#x20;

## Sample Script for getting starttime in JSON format

This script will format the current reference time (start time) and output it as JSON.

```liquid
{
    "clock": "{{ Model.UtcClock | object.format "O" }}",
    "starttime": {{ Model.IsRuntime ? "\"" + (Model.ReferenceTime | object.format "O") + "\"" : "null"  }},
    "runtime": {{ Model.IsRuntime ?  "\"" + Model.Runtime + "\"" : "null" }},
    "isStarted": {{ Model.IsRuntime ? "true":"false" }}  
}
```

The "O" formatter will output dates and times in JSON standard format including timezone.&#x20;
