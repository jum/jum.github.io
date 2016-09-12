# The cost of IP Traffic

## A Typical Scenario

In most modern apps the assumption is that IP traffic is basically free. Most desktop apps just use the Internet as they see fit. On mobile phones (iOS as per my experience) there is a way to find out if the device is connected via the mobile data network, which might be volume capped and thus expensive. Mobile apps do allow to postpone certain bulk data accesses to times when the device is connected via WIFI. A typical example is WhatsApp, which has a setting to perform chat backups only when connected via WIFI.

This distinction is only touching the surface of the problem. There are many scenarios where this all breaks down and many assumptions about the network type are meaningless. For example to say that a mobile link is expensive and a WIFI link is cheap (or even basically free) does only work locally on a device that has both of these connections and the WIFI connection (if connected) is connected to an unlimited flat data plan.

Even in a simple traveling arrangement this can produce surprisingly expensive and easy to do mistakes. Consider for example the following scenario: you travel with your Mac laptop, an iPhone (with volume capped data plan) and an iPad. While traveling you need to do some work on your laptop that requires internet connectivity, so as a cost conscientious human being you stop all your apps on the Mac laptop that are not supposed to be talking to the Internet right now and only start the app(s) you need right now.

But you still have the iPad in your backpack, and probably you have forgotten to turn off WIFI on that device. As soon as you turn on the hotspot feature on your phone, which is very easy to do nowadays that you can tether to your phone directly from the WIFI menu on the Mac, the iPad will probably connect to that hotspot as well and will tell the interested apps on that device that WIFI is available. In my case I did use the Apple WWDC app to download a few developers videos for offline viewing on my iPad. As I grabbed the iPad to put in the bag I did not check if all of those videos really completed downloading and the WWDC app started to resume a few of these downloads consuming all my precious data volume plan in no time.

Very similar mishaps can happen even with any mobile data connection shared via WIFI, like for example the typical MIFI devices sold all over the world to make small WIFI networks using a cellular connection. With iCloud password sharing all your devices now know how to connect far to easily and it is increasingly difficult to control which applications do perform network I/O and consume your data plan.

## What is missing here?

There are quite a few features missing in applications and the OS, and none of these have been addressed except some special cases, like limiting an NSURLSession to not use mobile data, which is really only a band aid.

To summarize:

* There is no way for apps to convey to the underlying API's of the OS beyond a certain quality of service as to why the data transfer is initiated (user initiated background, user initiated wants it right now).
* There is no way to guess the cost of an Internet connection in any sensible way for apps. Just saying mobile data is expensive and WIFI is cheap or even free is not the reality. The current guess work with mobile data vs. WIFI is just not the right way to do it.
* There needs to be a way to associate attributes to an Internet connection that are conveyed to client apps across the boundaries of WIFI or even connected networks, to make higher level decisions about planning data intense tasks. If my main uplink to the Internet is down and I am using a slower (and more expensive) backup link I might want to postpone a network backup to more opportune time unless it is really pressing and I said do it right now.
* There are very few controls for the user regarding to background activity of apps (especially with iOS). On the traditional desktop environment this is easy - just quit the app you do not want to be active and there will be no network traffic from that app. This will get more like on iOS considered that even desktop OSes now have API's to initiate background file transfers while the responsible app is not running.
