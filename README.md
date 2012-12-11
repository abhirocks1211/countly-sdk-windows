Countly SDK for Windows Phone
=============================

Countly Windows Phone SDK is developed by [Tom Myles](mailto:tom.m935@gmail.com), [Devran Eroğul](mailto:devran@gmail.com)
and [Orkun Senturk](mailto:orkun.senturk@8bitiz.com).

##What's Countly?

Countly is an innovative, real-time, open source mobile analytics application. 
It collects data from mobile devices, and visualizes this information to analyze 
mobile application usage and end-user behavior. There are two parts of Countly: 
the server that collects and analyzes data, and mobile SDK that sends this data 
(for iOS, Android, Windows Phone and Blackberry). Both parts are open source.

##Installing Countly SDK

* 1. Download Countly Windows Phone SDK
* 2. Extract all to any folder
* 3. Open Countly.sln file with Visual Studio 2012
* 4. You now have three projects in your solution : Countly (main SDK) , OpenUDID (dependency) and Countly Test quickstarter project.
* 5. Right click solution , click **"Manage NuGet Packages"**. Select Online and search for **Json.NET** and install it for Countly SDK project only. After installation completed, go to References of the Countly SDK project and check newtonsoft.json is added to references.
* 6. Right click Countly SDK project, click Properties, then at Application tab select appropriate **"Target Windows Phone OS Version"**. If you select Windows 7, please uncomment line 2 in Countly.cs in Countly project :


<pre class="prettyprint">
   #define WP8
</pre>

* 7. Right click Countly Test , click properties then at Application tab select **Target Windows Phone OS Version**. 

* 8. Go to **App.xaml** file in Countly Test project and update init method in **Application_Activated** and **Application_Deactivated** event handlers with your application key. There is third optional parameter at init method which you can use to send your application version number to countly. Final look should be like this :

<pre class="prettyprint">

   // Code to execute when the application is launching (eg, from Start)
        // This code will not execute when the application is reactivated
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
            System.Threading.ThreadPool.QueueUserWorkItem((o) =>
                {
                    Countly.Countly.SharedInstance().init("http://demo.count.ly", "YOUR_APP_KEY", "2.0");
                    Countly.Countly.SharedInstance().OnStart();
                });
        }

        // Code to execute when the application is activated (brought to foreground)
        // This code will not execute when the application is first launched
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
            System.Threading.ThreadPool.QueueUserWorkItem((o) =>
            {
                Countly.Countly.SharedInstance().init("http://demo.count.ly", "YOUR_APP_KEY", "2.0");
                Countly.Countly.SharedInstance().OnStart();
            });
        }
</pre>


* 9. Build solution and now you have ready for test your first application. Right click to Countly Test project and click **"Set as StartUp Project"**

* 10. You can run your application on a device or an emulator provided by Visual Studio Windows Phone 8 development kit.


Countly Server source code:

- [Countly Server (countly-server)](https://github.com/Countly/countly-server)

Other Countly SDK repositories:

- [Countly iOS SDK (countly-sdk-ios)](https://github.com/Countly/countly-sdk-ios)
- [Countly Android SDK (countly-sdk-android)](https://github.com/Countly/countly-sdk-android)
- [Countly Windows Phone SDK (countly-sdk-windows-phone)](https://github.com/Countly/countly-sdk-windows-phone)
- [Countly Blackberry Webworks SDK (countly-sdk-blackberry-webworks)](https://github.com/Countly/countly-sdk-blackberry-webworks)
