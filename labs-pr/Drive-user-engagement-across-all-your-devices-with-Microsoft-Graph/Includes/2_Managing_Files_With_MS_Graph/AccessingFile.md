# Accessing file data

What we are going to do in this module is to bring us the list of the most recent OneDrive documents, complementing the knowledge acquired in the Sample API Calls Module.


## Get my recent files from OneDrive from Graph API

In UWP project go to **Helpers/OneDriverHelper.cs** GetRecentItems method and follow the steps:

- Delete the code

	`throw new NotImplementedException();`

- Add the following code

         	List<DriveItem> filesName = new List<DriveItem>();

            try
            {
                var graphClient = AuthenticationHelper.GetAuthenticatedClient();

                var onedrive = graphClient.Me.Drive.Recent().Request().GetAsync().Result;
                filesName = onedrive.Take(10).ToList();
                return filesName;
            }

            catch (Exception ex)
            {
                Debug.WriteLine("Error get recent files in One Drive: " + ex.Message);
                throw;
            }

After get graphClient we can access to OneDrive via graphClient.Me.Drive and via Recent Method get the most recent files.


- Build and run the application.
- Click in Log in button to authenticate.
- After the authentication appears a **Recent File OneDrive** button. Click in this button.
- Appear in the applications the first ten documents that have been modified recently

![alt text](/labs-pr/Drive-user-engagement-across-all-your-devices-with-Microsoft-Graph/media/RecentFiles.png) 
