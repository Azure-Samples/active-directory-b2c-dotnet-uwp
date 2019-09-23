---
page_type: sample
languages:
- csharp
products:
- azure
description: "This simple sample demonstrates how to use the Microsoft Authentication Library (MSAL) for .NET to get an access token and call an API."
urlFragment: active-directory-b2c-dotnet-uwp
---

# Universal Windows Platform (UWP) application signing in users with Azure Active Directory B2C and calling an API

This simple sample demonstrates how to use the [Microsoft Authentication Library (MSAL) for .NET](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to get an access token and call an API secured by Azure AD B2C.
This sample is very similar to the [active-directory-b2c-dotnet-desktop](https://github.com/Azure-Samples/active-directory-b2c-dotnet-desktop) sample except that it's implemented for the UWP plaform instead of WPF.

## How To Run This Sample

To run this sample you will need:
- Visual Studio 2015
- An Internet connection
- At least one of the following accounts:
- An Azure AD B2C tenant

If you don't have an Azure AD B2C tenant, you can follow [those instructions](https://azure.microsoft.com/documentation/articles/active-directory-b2c-get-started/) to create one. 
If you just want to see the sample in action, you don't need to create your own tenant as the project comes with some settings associated to a test tenant and application; however it is highly recommend that you register your own app and experience going through the configuration steps below.   

### Step 1:  Clone or download this repository

From your shell or command line:

`git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-uwp.git`

### [OPTIONAL] Step 2: Create an Azure AD B2C application 

You can run the sample as is with its current settings, or you can optionally register it as a new application under your own developer account. Creating your own app is highly recommended.

> *IMPORTANT*: if you choose to perform one of the optional steps, you have to perform ALL of them for the sample to work as expected.

You can find detailed instructions on how to create a new mobile / native app on [this page](https://docs.microsoft.com/en-us/azure/active-directory-b2c/add-native-application) Make sure to:

- Copy down the **Application Id** assigned to your app, you'll need it in the next optional steps.
- Copy down the **Redirect URI** you configure for your app.

### [OPTIONAL] Step 3: Create your own policies

This sample requires your B2C app to the following policy types "Sign Up or Sign In", "Edit Profile" and "Reset Password".
You can follow the instructions in [this tutorial](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies) to create them.
Once created, replace the following value in the `App.xaml.cs` file with your own policy name.  All B2C policies should begin with `b2c_1_`.

```C#
public static string PolicySignUpSignIn = "b2c_1_susi";
```

### [OPTIONAL] Step 4: Create your own API

Our sample calls the Web API produced by the following sample [https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) (and pre-hosted in Azure). See the [README.md](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi/blob/master/README.md) file for that sample to understand better how to create your own Web API.

### [OPTIONAL] Step 5:  Configure the Visual Studio project with your app coordinates

1. Open the solution in Visual Studio 2015 or 2017.
1. Open the `App.xaml.cs` file.
1. Find the assignment for `public static string ClientID` and replace the value with the Application ID from Step 2.
1. Find the assignment for each of the policies `public static string PolicyX` and replace the names of the policies you created in Step 3.
1. Find the assignment for the scopes `public static string[] Scopes` and replace the scopes with those you created in Step 4.

### [OPTIONAL] Step 6:  Enable Windows Integrated Authentication when using a federated Azure AD tenant
Out of the box, this sample is not configured to work with Windows Integrated Authentication (WIA) when used with a federated Azure Active Directory domain. To work with WIA the application manifest must enable additional capabilities. These are not configured by default for this sample because applications requesting the Enterprise Authentication or Shared User Certificates capabilities require a higher level of verification to be accepted into the Windows Store, and not all developers may wish to perform the higher level of verification.
To enable Windows Integrated Authentication, in Package.appxmanifest, in the Capabilities tab, enable:
1. Enterprise Authentication
2. Private Networks (Client & Server)
3. Shared User Certificates

Also, in the constructor of the application in `App.xaml.cs`, add the following line of code: ```authContext.UseCorporateNetwork = true;```

### Step 7:  Run the sample

1. Clean the solution, rebuild the solution, and run it.
1. Click the sign-in button at the top of the application screen. The sample works exactly in the same way regardless of the account type you choose, apart from some visual differences in the authentication and consent experience. Upon successful sign in, the application screen will list some basic profile info for the authenticated user and show buttons that allow you to edit your profile, call an API and sign out.
1. Close the application and reopen it. You will see that the app retains access to the API and retrieves the user info right away, without the need to sign in again.
1. Sign out by clicking the Sign out button and confirm that you lose access to the API until the exit interactive sign in.  

## More information
For more information on Azure B2C, see [the Azure AD B2C documentation homepage](http://aka.ms/aadb2c). 
