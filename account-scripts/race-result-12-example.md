# RACE RESULT 12 Example

We want to query the start time from a contest in RR12 and use it as a start time in RemoteDisplay.&#x20;

## Configure RR12

Create an output list in RR12 with all the information you need, at the minimum the start time for your contest. Make it available externall via SImple API.

## Configure Account Script

In this script, we query the RR12 list. If we encounter a start time is set, then we set the starttime of the scene and also switch to a scene called "Runtime". If no start time is present, then we switch to a scene called "Clock".

```javascript

Script.onStart = () => {
    
}

Script.onStop = () => {
  
}

Script.onRefresh = function onRefresh() {
    log("OnRefresh");
    
    // Get link
    var link = Model.Account.GetLink("d184d831-9936-4ba6-321e-08dbceedad15");
    if (!link) 
        return;


    // Get url from a RR12 output list with at least one column called StartTime
    var url = "https://api.raceresult.com/370734/QUFZ34K3ZSYYJ5P0L4V7FVH5M9Y3CWRO";
    var response = httpGet(url);
    
    

    // Check for response status code and parse body to JSON
    if (response.IsSuccessStatusCode) {
        
        var json = JSON.parse(response.body);
	    if (json && json.length > 0) {   
	        var jsonStartTime = json[0].StartTime;
	        if (jsonStartTime.startsWith("00:00:00") || jsonStartTime == 0)
	            jsonStartTime = null;



            if (jsonStartTime) {
                link.SetStartTime(jsonStartTime);
                link.SetScene("Runtime");
            } else {
                link.SetScene("Clock");
            }

         
	    }
    } else {
        
        log("Invalid Response");
    }
    
};
```

## Scene Script

As the account script already sets the starttime, we can use regular script scenes.&#x20;
