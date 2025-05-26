# FDS MLED

## Display Blank

This script displays just blank digits on board A:

```
{{ 
    mled.CreateProtocol "        " 1 "Dark"
}}
```

## Display Clock

This script display the current time of day:

```
{{
    time = Model.Clock
    formatString = time.TimeOfDay.Seconds % 2 == 0 ? "HH:mm" : "HH mm"
    timestring = time | FormatRaceResult formatString
    timestring = timestring | TrimPad 8 "Center"
    color = "Blue"

    line = (mled.Color color) + timestring
    mled.CreateProtocol line 1 "Bright"
}}
```

## Display Clock, Countdown or Runtime depending on Reference Time

This script will display different information depending on the reference time:

* If reference time is not set it will show the current time of day
* If reference time is in the future it will show the countdown
* If reference time is in ther past it will show the runtime&#x20;

```liquid
{{
    if Model.ReferenceTime == null
        # No reference time set
        time = Model.Clock
        timestring = time | FormatRaceResult "HH:Mm:ss"
        color = "Blue"
    else if Model.Runtime && Model.Runtime.TotalSeconds > 0
        # After Start
        time = Model.Runtime
        timestring = time | FormatRaceResult "HH:Mm:ss"
        color = "White"
    else
        # Before Start
        time = Model.Countdown
        timestring = time | FormatRaceResult "HH:Mm:ss"
        color = "Purple"
    end
    timestring = timestring | TrimPad 8 "Right"
    timestring = (mled.Color color) + (timestring| TrimPad 8 "Center")
    mled.CreateProtocol timestring 1 "Dark"
}}
```

## Display Two Lines of Text

This script will display two lines of maximum 16 charaters.



```liquid
{{ 
    line1 = "Herzlich"
    line2 = "Willkommen" 
    
    line1 = line1 | TrimPad 16 "Center"
     line2 = line2 | TrimPad 16 "Center"
    
    mled.CreateProtocol line1 2 "Bright"
    mled.CreateProtocol line2 3 "Bright"
}}
```
