---
description: >-
  This link type is for sending display data that is either generated remotely a
  t some location or by RemoteRedirect webservice to a remotely deployed display
  board.
---

# Display

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="145"></th><th></th></tr></thead><tbody><tr><td>Display Type</td><td>Brand and make of the display type (not used at the moment)</td></tr><tr><td>Mode</td><td>Idle - do nothing<br>Scene - Send out link script output</td></tr><tr><td>Clock Offset</td><td>The offset to UTC time to allow for clocks in the current time zone</td></tr><tr><td>Target Time</td><td>Referecne or start time to be used for link scripts (usually only be configurd in <a href="live.md">Live</a> view)</td></tr><tr><td>Forward Timeout</td><td>When sending data from one location to another, sometimes the connection is severed to the input side. After a timeout, the output side is sent the current link script to not show outdated/old data</td></tr></tbody></table>
