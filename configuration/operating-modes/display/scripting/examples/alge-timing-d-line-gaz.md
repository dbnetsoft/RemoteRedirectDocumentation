# ALGE-Timing D-Line/GAZ

A short video on how to configure scripting for ALGE-Timing D-Lines can be found on the [dbnetsoft YouTube channel](https://www.youtube.com/channel/UCXYI2v8j8v2SRsVumkpd_1Q):&#x20;

{% embed url="https://www.youtube.com/watch?v=VeVRDPLIQcg" %}

## Display Blank

This script displays just blank digits:

```
{{ 
    gaz.CreateProtocol("", "", "", "");
}}
```

## Display Clock (w/ seconds)

This script display the current time of day:

```
{{ 
    address = "";
    bib = "";
    rank = "";
    clockString = gaz.Format(Clock, 0, true)
    gaz.CreateProtocol(address, bib, rank, clockString);
}}
```

## Display Clock (w/ blinking separator)

```
{{
    address = "";
    bib = "";
    rank = "";
    
    time = Model.Clock
    formatString = time.TimeOfDay.Seconds % 2 == 0 ? "HH:mm" : "HH mm"
    timeString = Clock | Format formatString 
    
    # Append blanks for .ss.fff
    timeString = timeString + "       "
    
    gaz.CreateProtocol(address, bib, rank, timeString);
}}
```

## Display Countdown

This script will show a countdown when reference is set and in the future. If reference time is not set it will just show the current time of day. If reference time is in the past it will show 0

```
{{ 
    address = "";
    bib = "";
    rank = "";

    if Model.ReferenceTime == null
        # No reference time set
        time = ToTimeSpan 0
    else if Model.Countdown && Model.Countdown.TotalSeconds > 0
        # After Start
        time = Model.Countdown
    else
        # Before Start
        time = ToTimeSpan 0
    end
    timeString = gaz.Format(time, 0, true)
   
    gaz.CreateProtocol(address, bib, rank, timeString);
}}
```

## Display Runtime

This script will show a running time when reference is set and is in the past. If reference time is not set it will show 0.

```
{{ 
    address = "";
    bib = "";
    rank = "";

    if Model.ReferenceTime == null
        # No reference time set
        time = ToTimeSpan 0
    else if Model.Runtime && Model.Runtime.TotalSeconds > 0
        # After Start
        time = Model.Runtime
    else
        # Before Start
        time = ToTimeSpan 0
    end
    timeString = gaz.Format(time, 0, true)
   
    gaz.CreateProtocol(address, bib, rank, timeString);
}}
```

## Display Clock, Countdown or Runtime depending on Reference Time

This script will display different information depending on the reference time:

* If reference time is not set it will show the current time of day
* If reference time is in the future it will show the countdown
* If reference time is in ther past it will show the runtime&#x20;

```
{{ 
    address = "";
    bib = "";
    rank = "";

    if Model.ReferenceTime == null
        # No reference time set
        time = Model.Clock
    else if Model.Runtime && Model.Runtime.TotalSeconds > 0
        # After Start
        time = Model.Runtime
    else
        # Before Start
        time = Model.Countdown
    end
    timeString = gaz.Format(time, 0, true)
   
    gaz.CreateProtocol(address, bib, rank, timeString);
}}
```

## Display Clock, Countdown or Runtime (with different formatting options)

```
{{ 
    address = "";
    bib = "";
    rank = "";

    if Model.ReferenceTime == null
        # No reference time set
        formatString = Model.Clock.TimeOfDay.Seconds % 2 == 0 ? "HH:mm" : "HH mm"
        timeString = Model.Clock | Format formatString
        timeString = timeString | TrimPad 8 "Right"
        timeString = timeString | TrimPad 12 "Left"
    else if Model.Runtime && Model.Runtime.TotalSeconds > 0
        # After Start
        timeString = Model.Runtime | Format  "hh:mM:SS.f"
 timeString = timeString | TrimPad 10 "Right"
        timeString = timeString | TrimPad 12 "Left"
    else
        # Before Start
        timeString = Model.Countdown | Format "hh:mM:SS"
        timeString = timeString | TrimPad 8 "Right"
        timeString = timeString | TrimPad 12 "Left"
    end

    gaz.CreateProtocol(address, bib, rank, timeString);
}}
```
