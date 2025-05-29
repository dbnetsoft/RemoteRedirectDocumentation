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

## Show running time for two competitions simultenously

This is useful for showing running times for two competitions on two lines (e.g. different starting blocks or men and women starting time delayed). The text to display and the starttime can be entered at the end of the script and are not taken from the link or scene's reference time.&#x20;

<figure><img src="../../.gitbook/assets/image (5).png" alt="" width="300"><figcaption></figcaption></figure>

{% hint style="info" %}
FDS MLED line nr 1 equals to one row with 8 characters, line nr 2 and 3 are the top and bottom row with two rows each 16 characters wide.&#x20;
{% endhint %}

```
{{

    # Defines a function to show a text and a running time on a specific line nr
    func showLine(text, starttime, lineNr) 
   
         # Trim and align the text left by 8 characters
        text = text | string.TrimPad 8 "Left"
        
        # Transform starttime into usble timespan
        starttime = starttime | timespan.ParseTimeOfDay
        
        # Calculate the difftime to the current time in seconds
        diff = Clock.TimeOfDay.TotalSeconds - starttime.TotalSeconds
        
        # Decide what to do before starttime or after
        if (diff >= 0)
            diff = FormatRaceResult diff "HH:Mm:ss"
        else 
            diff = "-"
        end
        
          # Trim and align the time right by 8 characters
        diff = diff | string.TrimPad 8 "Right"
        
    
        # Construct the line to display
        line = (mled.Color "Red") + text + (mled.Color "White") + diff
      
        # Construct the FDS MLED specific string and return it
        mled.CreateProtocol line lineNr
   
    end 

    # Call the defined function with the repsective parameters
    showLine("M Bl. A", "14:45:22,2", 2)
    showLine("M Bl. B", "14:50:25,1", 3)

}}
```
