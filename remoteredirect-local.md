---
description: >-
  Windows program that connects a serial port or a local TCP device to one side
  of a link.
---

# RemoteRedirect Local

RemoteRedirect Local runs on a Windows PC and forwards data in both directions between a port on that PC and one side of a [link](general/wording.md). Use it when the device that sends or receives the data is connected to a PC instead of a router or a phone, for example:

* a timing device on an RS232 port that feeds the input of a link,
* a display board on the serial port of a PC that shows the output of a link,
* a program on the PC or in the local network that sends or receives data over TCP.

## Download

[Download RemoteRedirect Local](https://downloads.dbnetsoft.com/remoteredirect/RemoteRedirectLocal.exe). It is a single program file, there is nothing to install. The same download is offered on your dashboard on the RemoteRedirect website.

Requirements:

* Windows 10 or 11, 64-bit
* The [.NET 10 Desktop Runtime (x64)](https://dotnet.microsoft.com/download/dotnet/10.0). If it is missing, Windows shows a message with a download link when the program starts.
* The network must allow outgoing TCP connections to **links.remoteredirect.com** on the port of the link side.

## Input side and output side of a link

Every link has two sides, the **input** and the **output**. Each side is a port on the RemoteRedirect server.

When a side is set to **TCP server** in the settings of the link, RemoteRedirect opens a TCP port for it on **links.remoteredirect.com** and waits there for connections. Every link side has its own port number. Devices and programs connect to that port as TCP clients: RemoteRedirect Local, a [mobile RS232 router](configuration/operating-modes/display/connectivity/mobile-rs232-router.md), an RS232-to-Ethernet converter or a timing program.

What arrives on one side is passed on to the other side:

* Data a client sends to the **input** is sent to every client connected to the **output**.
* Data a client sends to the **output** is sent to every client connected to the **input**.
* On a [Display](configuration/operating-modes/display/) link, the **output** also receives the display data RemoteRedirect generates from the selected scene, whenever nothing has arrived on the input for a while.

So the input is usually where the data comes from (a timing device, results software) and the output is where it goes to (a display board, receiving software). In RemoteRedirect Local, choose the side by what is connected to your PC:

| Connected to your PC                                                    | Side to choose |
| ----------------------------------------------------------------------- | -------------- |
| The device or program that produces the data, e.g. a timing device      | Input          |
| The device or program that shows or uses the data, e.g. a display board | Output         |

{% hint style="info" %}
* Only a side set to **TCP server** can be connected to. If a side is a serial port or a TCP client in the settings of the link, RemoteRedirect itself connects out on that side, and RemoteRedirect Local shows the side as not available.
* **www.remoteredirect.com** is only the website. The ports of the links are reached through **links.remoteredirect.com**.
* Each side accepts up to five clients unless set otherwise. Further connections are closed with the message TOO MANY CONNECTIONS.
* The port numbers are shown on the [Live](configuration/operating-modes/display/live.md) page of the link. RemoteRedirect Local finds them by itself: you only choose the link and the side.
{% endhint %}

## Setting up forwarding

1. **Sign in.** Click _Sign in_ and enter the email address and password of your RemoteRedirect user account. If your account uses two-factor authentication, also enter the code of your authenticator app. Tick _Remember password_ to have the sign-in renewed automatically after 14 days. This does not work for accounts with two-factor authentication, they sign in again after 14 days.
2. **Choose the local port** on the left:
   * **Serial** - the RS232 port and its baud rate. A USB-RS232 adapter shows up as a COM port.
   * **TCP Client** - host name or IP address and port of a device in your network to connect to, e.g. an RS232-to-Ethernet converter.
   * **TCP Server** - a port on your PC that other programs connect to.
3. **Choose the link and the side** on the right. The list shows all links of your accounts. Next to each side you see its TCP port and how many clients are connected.
4. Click **Start**.

The bars above the local port and the RemoteRedirect side show the connection: green when connected, orange while connecting, red when not connected. The local port and the link cannot be changed while forwarding is running, click _Stop_ first.

## Monitor

The table at the bottom lists every block of data that was forwarded, with time, direction, number of bytes and the data itself. Control characters are written by name, e.g. `<STX>`, `<CR>` or `<LF>`. _Show hex_ adds the bytes in hexadecimal, _Pause monitor_ stops adding data while connection changes are still listed.

The counters in the top right show the bytes sent to RemoteRedirect, sent to the local port, and dropped. Data is dropped when the other side is not connected, e.g. when the local port is a TCP server and no program is connected to it.

## Profiles

The name of the current profile is shown in the title bar. Click it to create a new profile, load one, save it or save it under another name. Profiles are files ending in `.RemoteRedirectLocalConfig`.

A profile stores the local port, the link and the side, and whether forwarding was running. A profile that was running when the program was closed starts forwarding again when it is opened, e.g. after the PC restarted.

The sign-in is not part of a profile. It is stored encrypted for the Windows user, so profiles can be passed on to others.

## Good to know

* Forwarding keeps running when the RemoteRedirect website cannot be reached or the sign-in has expired: the program remembers the last port of the link side.
* While signed in, the program checks the link every 30 seconds and follows when the port of the side changes.
* Expired links cannot be connected.
* Only one instance of the program runs at a time.
* _File - Settings_ changes the theme and the language.
