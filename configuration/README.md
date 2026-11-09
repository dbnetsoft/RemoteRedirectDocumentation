# Links

A link carries data between two sides, the **input** and the **output**. Data that arrives on one side is passed on to the other. What a link does with the data in between depends on its [operating mode](operating-modes/), how it is set up is described under [Settings](settings.md).

## Ways to connect

| Way                                                                                                                                                                                     | Connects to                                                                                                                                    | Use it for                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [RemoteRedirect app](operating-modes/display/connectivity/android-app.md) on Android, iPhone or iPad                                                                                    | The web service (www.remoteredirect.com) - **not** a TCP port of the link                                                                      | [Display](operating-modes/display/) links. The app produces the display data itself and drives the display board through a USB-RS232 adapter, a network converter or a [Bluetooth adapter](../app/bluetooth-adapters.md). It keeps running when the internet connection is poor. |
| [RemoteRedirect Local](../remoteredirect-local.md) on a Windows PC                                                                                                                      | The TCP port of the input or the output on links.remoteredirect.com. You sign in and choose the link and the side, the program finds the port. | A device on the serial port of a PC, or a program on the PC or in the local network.                                                                                                                                                                                             |
| [RS232 router](operating-modes/display/connectivity/mobile-rs232-router.md) or RS232-to-Ethernet converter, e.g. [Teltonika](../readme/hardware/teltonika-trb142-rut956/) or Moxa NPort | The TCP port of the input or the output on links.remoteredirect.com, as a TCP client                                                           | A display board or a timing device on site without a PC.                                                                                                                                                                                                                         |
| Your own software                                                                                                                                                                       | The TCP port of the input or the output on links.remoteredirect.com, as a TCP client                                                           | Any program that can open a TCP connection.                                                                                                                                                                                                                                      |

## Connecting over TCP

### Input side and output side

Each side of a link has a port type. It is set up by dbnetsoft when the link is created; contact us to change it.

| Port type of the side       | What RemoteRedirect does                                                    | What you set up on your device                                                                                                 |
| --------------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **TCP server** (most links) | Opens a TCP port on **links.remoteredirect.com** and waits for connections. | Your device or program connects to it as a **TCP client**: host links.remoteredirect.com, port of the side.                    |
| **TCP client**              | Connects out to a host name and port that are stored in the link.           | Your device must be reachable from the internet on that port (public IP address or port forwarding) and accept the connection. |

What arrives on one side is passed on to the other side:

* Data a client sends to the **input** is sent to every client connected to the **output**.
* Data a client sends to the **output** is sent to every client connected to the **input**.
* On a [Display](operating-modes/display/) link, the **output** also receives the display data RemoteRedirect generates from the selected scene, whenever nothing has arrived on the input for a while.

So the input is usually where the data comes from (a timing device, results software), and the output is where it goes to (a display board, receiving software).

### Host name

Connect to **links.remoteredirect.com**.

{% hint style="warning" %}
**www.remoteredirect.com** is only the website. It is behind a proxy that only passes web traffic, so a device configured with www.remoteredirect.com cannot connect to the port of a link.
{% endhint %}

### Port numbers

Every side has its own port number, e.g. 5005 for the input and 5006 for the output of a link. You find them on the [Live](operating-modes/display/live.md) page of the link: _TCP In_ followed by the port number for a side that is a TCP server, _TCP Out_ followed by host name and port for a side that is a TCP client. RemoteRedirect Local shows them next to the side as well.

### Good to know

* The connection is plain TCP: the bytes are passed on as they are, without login, handshake or encryption on the port. Anyone who knows the port number can connect, so only give it to the people who need it.
* Each side accepts up to five clients unless agreed otherwise. Further connections receive TOO MANY CONNECTIONS and are closed.
* A connection is closed right away when its first data looks like a web, remote desktop or similar request. These come from scanners on the internet, not from timing devices or display boards.
* When a link has expired, its ports are closed.
* The network on site must allow outgoing TCP connections to links.remoteredirect.com on the port numbers of the link. Some company and event networks block ports other than those for the web; a mobile connection usually works.
* Devices should reconnect on their own when the connection drops. For routers and converters, set a reconnect interval, e.g. 30 seconds.
