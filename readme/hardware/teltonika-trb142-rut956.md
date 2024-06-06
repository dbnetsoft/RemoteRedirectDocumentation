# Teltonika TRB142/RUT956

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

|                     |       |
| ------------------- | ----- |
| Raw Mode            | on    |
| No leading zeros    | off   |
| Reconnect interval  | 30    |
| Inactivity timeout  | 0     |
| Serial timeout      | empty |
| TCP Echo            | off   |
| Close connections   | off   |
| Connect on data     | off   |
| Keep alive time     | 0     |
| Keep alive interval | 0     |
| Keep alive probes   | 0     |

More information on Teltonika TRB142 can be found [here](teltonika-trb142.md).
