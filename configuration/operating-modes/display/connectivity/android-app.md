# Android App

## Overview

<figure><img src="../../../../.gitbook/assets/Remote Redirect Phone.png" alt=""><figcaption><p>Setup diagram</p></figcaption></figure>

The Android app establishes a connection to the RemoteRedirect web service and a specific link.&#x20;

The Android App receives any changes from the RemoteRedirect web service in terms of reference time changes, script changes on scene changes. All the data is sent to the display board is produced locally, and therefore does not need stable internet connection for it. Only when needing to react on changes an internet connection is required.&#x20;

## USB-RS232 Adapters

The data from the app to the displayboard is usually via RS232. Therefore you need to connect an USB-RS232 adapter to your phone.&#x20;

The following adapters have been confirmed working with our Android app:

* DriverGenius 1-Port UBS Adapter USB-A ([Amazon](https://www.amazon.de/gp/product/B0BYRW5J4K/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8\&psc=1))
* DriverGenius 1-Port USB Adapter USB-C ([Amazon](https://www.amazon.de/gp/product/B07Y33RHB2/ref=ppx_yo_dt_b_asin_title_o02_s01?ie=UTF8\&psc=1))

## Download

The app can be downloaded from the Google Play Store.

{% embed url="https://play.google.com/store/apps/details?id=com.dbnetsoft.RemoteRedirect" %}
Google Play Store Download
{% endembed %}
