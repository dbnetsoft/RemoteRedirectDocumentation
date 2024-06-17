# Configuration

You usually find the settings for the serial port under _Services_ - _Serial Utilities_ - _Over IP._&#x20;

There you need to define a configurationb as follows:&#x20;

| Parameter    | Value                                                                       |
| ------------ | --------------------------------------------------------------------------- |
| Device       | rs232                                                                       |
| Baudrate     | Depending on the display board (usually 2400 for ALGE or 9600 for FDS MLED) |
| Data Bits    | 8                                                                           |
| Stop Bits    | 1                                                                           |
| Parity       | None                                                                        |
| Flow Control | None                                                                        |
| Echo         | off                                                                         |

Under _General Tab_ set the following:

|                     |                                                     |
| ------------------- | --------------------------------------------------- |
| Mode                | Client                                              |
| Protocol            | TCP                                                 |
| Destination Address | www.remoteredirect.com                              |
| Destination Port    | Depending on your link, use number from Output side |

Under _Advanced Tab_ set the following:

<table><thead><tr><th width="454"></th><th></th></tr></thead><tbody><tr><td>Raw Mode</td><td>on</td></tr><tr><td>No leading zeros</td><td>off</td></tr><tr><td>Reconnect interval</td><td>30</td></tr><tr><td>Inactivity timeout</td><td>0</td></tr><tr><td>Serial timeout</td><td>empty</td></tr><tr><td>TCP Echo</td><td>off</td></tr><tr><td>Close connections</td><td>off</td></tr><tr><td>Connect on data</td><td>off</td></tr><tr><td>Keep alive time</td><td>0</td></tr><tr><td>Keep alive interval</td><td>0</td></tr><tr><td>Keep alive probes</td><td>0</td></tr></tbody></table>

More information on Teltonika TRB142 can be found [here](../teltonika-trb142.md).
