# Microgate Microtab

## Display Blank

This script displays just blank digits:

```
{{ 
    rowAddress = 'A'    # A is first row, B second row, ...
    columnIndex = 0     # 0 is first column, 1 is second column, ...
    columns = 10        # total amount of columns depending on the font setup
    
    text = ""
    text = text | TrimPad columns "Center"

    microtab.CreateAlphaStringProtocol(rowAddress, columnIndex, text)
}}
```

## Display Clock

This script display the current time of day:

```
{{ 
    rowAddress = 'A'    # A is first row, B second row, ...
    columnIndex = 0     # 0 is first column, 1 is second column, ...
    columns = 10        # total amount of columns depending on the font setup
    
    text = Link.Clock | Format "HH:mm:ss"
    text = text | TrimPad columns "Center"

    microtab.CreateAlphaStringProtocol(rowAddress, columnIndex, text)
}}
```

## Display Countdown

This script will show a countdown when reference is set and in the future. If reference time is not set it will just show the current time of day. If reference time is in the past it will show 0

```
{{ 
    rowAddress = 'A'    # A is first row, B second row, ...
    columnIndex = 0     # 0 is first column, 1 is second column, ...
    columns = 10        # total amount of columns depending on the font setup

    if Link.ReferenceTime == null
        # No reference time set
        text = Link.Clock  | Format "HH:mm:ss"
    else if Link.Runtime && Link.Runtime.TotalSeconds > 0
        # After Start
        text = ToTimeSpan 0  | Format "HH:mm:ss"
    else
        # Before Start
        text = Link.Countdown  | Format "HH:mm:ss"
    end
 
    text = text | TrimPad columns "Center"  
   
    microtab.CreateAlphaStringProtocol(rowAddress, columnIndex, text)
}}
```

## Display Runtime

This script will show a running time when reference is set and is in the past. If reference time is not set it will show 0.

```
{{ 
    rowAddress = 'A'    # A is first row, B second row, ...
    columnIndex = 0     # 0 is first column, 1 is second column, ...
    columns = 10        # total amount of columns depending on the font setup

    if Link.ReferenceTime == null
        # No reference time set
        text = ""
    else if Link.Runtime && Link.Runtime.TotalSeconds > 0
        # After Start
        text = ToTimeSpan 0  | Format "HH:mm:ss"
    else
        # Before Start
        text = Link.Countdown  | Format "HH:mm:ss"
    end
 
    text = text | TrimPad columns "Center"  
   
    microtab.CreateAlphaStringProtocol(rowAddress, columnIndex, text)
}}
```

## Display Clock, Countdown or Runtime depending on Reference Time

This script will display different information depending on the reference time:

* If reference time is not set it will show the current time of day
* If reference time is in the future it will show the countdown
* If reference time is in ther past it will show the runtime&#x20;

```
{{ 
    rowAddress = 'A'    # A is first row, B second row, ...
    columnIndex = 0     # 0 is first column, 1 is second column, ...
    columns = 10        # total amount of columns depending on the font setup

    if Link.ReferenceTime == null
        # No reference time set
        time = Link.Clock
    else if Runtime && Runtime.TotalSeconds > 0
        # After Start
        time = Link.Runtime
    else
        # Before Start
        time = Link.Countdown
    end
    time = time | Format "HH:mm:ss"
    text = time | TrimPad columns "Center"  
   
    microtab.CreateAlphaStringProtocol(rowAddress, columnIndex, text)
}}
```
