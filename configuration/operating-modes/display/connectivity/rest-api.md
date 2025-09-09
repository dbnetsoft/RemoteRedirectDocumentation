# REST API

The output of a display script can also be accessed via an HTTP GET call to `https://www.remoteredirect.com/api/links/{linkId}/output`

This can be useful when not feeding display boards with data but any other external software with HTTP capabilities.&#x20;

This is also very useful when connecting our ScreensPro videowall solution with RemoteRedirect. ScreensPro Server will constantly query the API for an updated start time and then display it in the layout accordingly.&#x20;

## Sample Script for getting starttime in JSON format

### RemoteRedirect Script

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

### ScreensPro Layout

The layout file in ScreensPro will be usiong the Sources feature Http that will constantly querying the RemoteRedirect output.&#x20;

* Add a new _HTTP Rest (JSON)_ source in _Sources_ - _+_
* Add the URL of your RemoteRedirect and name it _Link_

In the layout file, you can start a running time by using&#x20;

```
<seuc:Stopwatch2Element Foreground="White" FontSize="80" FontWeight="Bold" TextAlignment="Center" StartTime="{Binding Sources.Link.Value.starttime.TimeOfDay}" RunningFormat="hh:mM:ss" IsPaused="False"></seuc:Stopwatch2Element>
```

By using value converterts, you can also show the clock before start time and runtime after the start:

```
<!-- Before Start -->
<Grid Visibility="{Binding Sources.Link.Value.isStarted, Converter={StaticResource ObjectToVisibilityConverter}, ConverterParameter=false}">
    <seuc:ClockElement Foreground="White" FontSize="80" FontWeight="Bold" TextAlignment="Center"></seuc:ClockElement>
</Grid>

<!-- After Start -->
<Grid Visibility="{Binding Sources.Link.Value.isStarted, Converter={StaticResource ObjectToVisibilityConverter}}">
    <seuc:Stopwatch2Element Foreground="White" FontSize="80" FontWeight="Bold"  TextAlignment="Center" StartTime="{Binding Sources.Link.Value.starttime.TimeOfDay}" RunningFormat="hh:mM:ss" IsPaused="False"></seuc:Stopwatch2Element>
</Grid>
```
