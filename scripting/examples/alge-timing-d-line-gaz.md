# ALGE-Timing D-Line/GAZ

## Display Blank

This script displays just blank digits:

```
{{ 
    gaz.CreateProtocol("", "", "", "");
}}
```

## Display Clock

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

## Display Countdown

This script will show a countdown when reference is set and in the future. If reference time is not set it will just show the current time of day. If reference time is in the past it will show 0

```
{{ 
    address = "";
    bib = "";
    rank = "";

    if ReferenceTime == null
        # No reference time set
        time = Clock
    else if Runtime && Runtime.TotalSeconds > 0
        # After Start
        time = ToTimeSpan 0
    else
        # Before Start
        time = Countdown
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

    if ReferenceTime == null
        # No reference time set
        time = ToTimeSpan 0
    else if Runtime && Runtime.TotalSeconds > 0
        # After Start
        time = Runtime
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

    if ReferenceTime == null
        # No reference time set
        time = Clock
    else if Runtime && Runtime.TotalSeconds > 0
        # After Start
        time = Runtime
    else
        # Before Start
        time = Countdown
    end
    timeString = gaz.Format(time, 0, true)
   
    gaz.CreateProtocol(address, bib, rank, timeString);
}}
```
