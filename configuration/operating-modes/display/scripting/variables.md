# Variables

## Model

The variable `Model` is available in every scene script and has the following properties.&#x20;

In Script: `Model.`_`NameOfVariable`_

<table><thead><tr><th>Name</th><th width="165">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>Model.Clock</code></td><td>DateTimeOffset</td><td>Current time of day including optional time offset  set on link</td></tr><tr><td><code>Model.UtClock</code></td><td>DateTimeOffset</td><td>Current time in UTC</td></tr><tr><td><code>Model.ReferenceTime</code></td><td>DateTimeOffset?</td><td>Reference time set on link. Usually this is the start time of day</td></tr><tr><td><code>Model.HasRerenceTime</code></td><td>Bool</td><td>Checks for a rference time is set</td></tr><tr><td><code>Model.Countdown</code></td><td>TimeSpan?</td><td>Current countdown if reference time is set reference time is in the future</td></tr><tr><td><code>Model.IsCountdown</code></td><td>Bool</td><td>Checks for is before reference time</td></tr><tr><td><code>Model.Runtime</code></td><td>TimeSpan?</td><td>Current runtime if reference time is set and reference time is in the past</td></tr><tr><td><code>Model.IsRuntime</code></td><td>Bool</td><td>Checks for is after reference time</td></tr></tbody></table>

## Model.Scene

This variable holds information on the currently selected scene.

In Script: `Model.Scene.`_`NameOfVariable`_

<table><thead><tr><th>Name</th><th width="165">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>Model.Scene.UserDesxcription</code></td><td>String?</td><td>User given name of the scene</td></tr><tr><td><code>Model.Scene.DisplayTargetTime</code></td><td>DateTimeOffset</td><td>Target timeo f the scene only</td></tr></tbody></table>
