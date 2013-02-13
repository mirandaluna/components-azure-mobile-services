##Getting Started

To use Mobile Services with your iOS app, you will need a Windows Azure account.  If you already have an account, login to the [Windows Azure management portal](https://manage.windowsazure.com/).  If you are new to Windows Azure, you can sign up for a 90-day free trial [here](https://www.windowsazure.com/en-us/pricing/free-trial/).

To create a new Mobile Service after you've logged into the [management portal](https://manage.windowsazure.com/), select 'New' --> 'Compute' --> 'Mobile Service' --> 'Create.'  

![](WAMS-New.png)

Even though you will write the majority of your application in your preferred IDE, the management portal provides an easy way to work with three key Mobile Services features: storing data in the cloud, settuing up user authentication via third party services like Facebook, and sending push notifications.

You can find the full Getting Started with Mobile Services tutorial [here](https://www.windowsazure.com/en-us/develop/mobile/tutorials/get-started/).

## Connect a Mobile Service to your MonoTouch app written in C# 

After you've created a Mobile Service, use the following to connect your project:

```csharp
    using Microsoft.WindowsAzure.MobileServices;
...
public static MobileServiceClient MobileService = new MobileServiceClient(
"https://yourMobileServiceName.azure-mobile.net/", 
"YOUR_APPLICATION_KEY"
);
```

You can find value of your Mobile Service URL on the right-hand side of Dashboard and the value of your app key by clicking 'Manage Keys' at the bottom of the Dashboard.

To store data in that table, use the following code snippet (originally from the [September 2012 announcement](http://blog.xamarin.com/xamarin-partners-with-microsoft-to-support-azure-mobile-services-on-android-and-ios/) of the Xamarin and Windows Azure partnership):

```csharp 
    public class TodoItem
    {
        public int Id { get; set; }
        [DataMember (Name = "text")]
        public string Text { get; set; }
        [DataMember (Name = "complete")]
        public bool Complete { get; set; }
    }
    ...
    this.table = MobileService.GetTable<TodoItem>();
    this.table.Where (ti => !ti.Complete).ToListAsync()
            .ContinueWith (t => { this.items = t.Result; }, scheduler);
```

### Documentation

- Tutorials: https://www.windowsazure.com/en-us/develop/mobile/resources/
- Developer Center: http://www.windowsazure.com/mobile
- API Library: http://msdn.microsoft.com/en-us/library/windowsazure/jj710108.aspx
- Mobile Services GitHub Repo: https://github.com/WindowsAzure/azure-mobile-services
- Xamarin Mobile Services client framework GitHub Repo: https://github.com/xamarin/azure-mobile-services

### Contact

- Developer Forum: http://social.msdn.microsoft.com/Forums/en-US/azuremobile/threads
- Feature Requests: http://mobileservices.uservoice.com
- Contact: mobileservices@microsoft.com
- Twitter: @joshtwist @cloudnick @chrisrisner @mlunes90

###Legal 

- Terms & Conditions: http://www.windowsazure.com/en-us/support/legal/
