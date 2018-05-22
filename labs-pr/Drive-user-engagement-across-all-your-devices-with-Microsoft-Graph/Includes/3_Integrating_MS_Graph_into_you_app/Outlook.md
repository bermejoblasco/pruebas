# Integrating with office

But not only can we integrate with OneDrive, we can also integrate with the entire Office package through Graph API, in this section we will see how we can interact with Outlook to get contacts and to schedule events in the calendar.

## Get Personal contacts from outlook

In UWP project go to **OutlookHeñper.cs** GetContacts method and follow the steps:

- Delete the code

	`throw new NotImplementedException();`

- Add the following code

            try
            {
                var graphClient = AuthenticationHelper.GetAuthenticatedClient();
                return await graphClient.Me.Contacts.Request().GetAsync();
            }

            catch (Exception ex)
            {
                Debug.WriteLine("Error get contacts files in OneDrive: " + ex.Message);
                throw;
            }

- Build and run the application.

- Click in Log in button.

- Select **Outlook Contacts** option in menu

- You can see the name and email on you outlook contacts

![alt text](/labs-pr/Drive-user-engagement-across-all-your-devices-with-Microsoft-Graph/media/OutlookContacts.png) 

## Create a Schedule events in outlook 

In UWP project go to **OutlookHeñper.cs** SetAppintment method and follow the steps:

- Delete the code

	`throw new NotImplementedException();`

- Add the following code

            try
            {
                var graphClient = AuthenticationHelper.GetAuthenticatedClient();
                var start = new DateTimeTimeZone();
                start.DateTime = startCombo.ToString();
                start.TimeZone = TimeZoneInfo.Local.StandardName;

                var end = new DateTimeTimeZone();
                end.DateTime = endCombo.ToString();
                end.TimeZone = TimeZoneInfo.Local.StandardName;

                var evt = new Event()
                {
                    Subject =subject,
                    Start = start,
                    End = end
                };
                await graphClient.Me.Events.Request().AddAsync(evt);
            }

            catch (Exception ex)
            {
                Debug.WriteLine("Error set appintmen files in OneDrive: " + ex.Message);
                throw;
            }


- Build and run the application.

- Click in Log in button.

- Select **Scheule event in Outlook** option in menu

- Add a subject, select init date and hour and select end date and hou

- Click in Sechedule Event

![alt text](/labs-pr/Drive-user-engagement-across-all-your-devices-with-Microsoft-Graph/media/EventCalendar.png) 

- If you go to outlook calendar you can see the event.