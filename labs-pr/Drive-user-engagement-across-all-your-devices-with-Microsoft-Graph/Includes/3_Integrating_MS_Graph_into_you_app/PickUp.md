# Advance app feature

Timeline is linked to pick up where you left off, when you create an activity and session if we open Cortana offers you open  the applications to continue working.

## Pick up where you left off

Close the application and open **Cortana** you see:


![alt text](/labs-pr/Drive-user-engagement-across-all-your-devices-with-Microsoft-Graph/media/Cortana.png) 

If we click the application it opens

## Deep Link

At this point the applications open in Login init page.
If we want continue working where we left, we need pass arguments to our application.
In the module before, when we create the Activity we have this line:

 	userActivity.ActivationUri = new Uri($"holmicrosoftgraph://{UserExtensionHelper.option}");

In activation Uri pass a option, at this point always is empty. Go to save where we are.

In UWP project go to **Helpers/UserExtensionHelper.cs** PickupWhereYouLeft method and follow the steps:

- Add the code


			try
            {
                UserExtensionHelper.option = pickUpOption;
                await UserExtensionHelper.CreateActivity();
            }
            catch (Exception ex)
            {
                Debug.WriteLine("Error to create activity in graph: " + ex.Message);
                throw;
            }

- Build and run the application.

- Click in Log in button.

- Select any option.

- Close the application.

- Open Cortana ann in Pick up where you left off.

- And open the app.

- The app opens where we are.

We can save information in OneDrive how we learn before to save the state of the application.

> **Cross Platform:** Thanks to Microsoft Graph Activities we can open the application in Android or iOS in the same point that left off in our UWP. If you want learn more about how do it visit this [link](https://github.com/Microsoft/project-rome).