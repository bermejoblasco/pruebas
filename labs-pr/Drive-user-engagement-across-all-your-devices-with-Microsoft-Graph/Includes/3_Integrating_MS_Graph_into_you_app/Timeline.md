# Writing to the Timeline

Timeline is a new feature in Microsoft Graph API that eneable to store the state of you application when a person want to continue those activiites accros multiple devices.
To do that, Mircosoft Graph API enable a UserActivites that enable user back into the applications.
In this module learn how works UserActivities and show timeline in Windows.

## Create and Save an Activity in Windows

In UWP project go to **UserExtensionHelper.cs** CreateActivity method and follow the steps:

- Delete the code

	`throw new NotImplementedException();`

- Add the following code

       	public static async Task CreateActivity()
        {
            try
            {           
                UserActivitySession currentActivity;
                UserActivityChannel channel = UserActivityChannel.GetDefault();

                UserActivity userActivity = await channel.GetOrCreateUserActivityAsync("HOLMicroGraph");

                var adaptiveCard = File.ReadAllText($@"{Package.Current.InstalledLocation.Path}\AdaptiveCard.json");
                adaptiveCard = adaptiveCard.Replace("{{backgroundImage}}", "https://cdn.graph.office.net/prod/GraphDocuments/en-us/concepts/images/microsoft_graph.png");
                adaptiveCard = adaptiveCard.Replace("{{name}}", "Hands-on Lab Microsoft Graph");
                userActivity.VisualElements.DisplayText = "HOL Microsoft Graph";
                userActivity.ActivationUri = new Uri($"holmicrosoftgraph://{UserExtensionHelper.option}");
                userActivity.VisualElements.Content = AdaptiveCardBuilder.CreateAdaptiveCardFromJson(adaptiveCard);

                await userActivity.SaveAsync();
                //currentActivity = userActivity.CreateSession();
            }
            catch (Exception ex)
            {
                Debug.WriteLine("Error to create activity in graph: " + ex.Message);
                throw;
            }
        }


## Create a Session in Windows

Well, now we are save an activity but we are no create a session, we need creata a user session acitvity for the user for save the state of the app.

In the code before uncomment the line

	//currentActivity = userActivity.CreateSession();

- Build and run the application.

- Click in Log in button.

- Select **Add in Timeline** option in menu

- Click in Create Activity.

![alt text](/labs-pr/Drive-user-engagement-across-all-your-devices-with-Microsoft-Graph/media/CreateActivity.png) 

Now we go to task view in windows.

![alt text](/labs-pr/Drive-user-engagement-across-all-your-devices-with-Microsoft-Graph/media/TaskView.png) 


And we can see the applications in in Timeline, if we close the app and click in Timeline app card the application will be opened.

![alt text](/labs-pr/Drive-user-engagement-across-all-your-devices-with-Microsoft-Graph/media/Timeline.png) 

> **Note:** For timeline we use **Adaptive Card** to show the app in Timeline. You can learn more about **Adaptive Card** [here](http://adaptivecards.io/).
