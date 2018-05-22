# Using OneDrive for app data storage

Now that we have learned how to interact with OneDrive, one of the options we have is to save the information of our application in OneDrive: settings, images, documents, backups ..., 

So that if we install the application in another device we can recover all the information and settings we had.

Specifically in this section we are going to simulate how to save settings in OneDrive and how to recover them after a clean installation.

## Set settings app in OneDrive

In UWP project go to **DataSyncHelper.cs** SaveSettingsInOneDrive method and follow the steps:

- Delete the code

	`throw new NotImplementedException();`

- Add the following code

          try
            {
                var model = JsonConvert.SerializeObject(settingsModel);
                var graphClient = AuthenticationHelper.GetAuthenticatedClient();
          
                using (var contentStream = GenerateStreamFromString(model))
                {
                    var uploadedItem = await graphClient
                                                 .Drive
                                                 .Root
                                                 .ItemWithPath($"Hol/Graph/Settings/settings.txt")
                                                 .Content
                                                 .Request()
                                                 .PutAsync<DriveItem>(contentStream);
                }
            }
            catch (Exception ex)
            {
                Debug.WriteLine("Error get upload settings file in OneDrive: " + ex.Message);
                throw;
            }

- Build and run the application.

- Click in Log in button.

- Select **Save App Data in OneDrive** option in menu

- Active all options

- Click in Save Setting button

![alt text](/labs-pr/Drive-user-engagement-across-all-your-devices-with-Microsoft-Graph/media/SaveAppData.png)

- Now go to your OneDrive and you can see the file settings.txt was created in HOL/Graph/Settings. This file contains the app settings

## Restore settings when install the app

Now we need uninstall our UWP app. Search Microsfot.Graph.HOL App, right click and uninstall.

No in UWP project go to **DataSyncHelper.cs** GetSettingsInOneDrive method and follow the steps:

- Delete the code

	`return new SettingsModel();

- Add the following code

            try
            {                
                var graphClient = AuthenticationHelper.GetAuthenticatedClient();

                var settingsStream = await graphClient
                                                .Drive
                                                .Root
                                                .ItemWithPath($"Hol/Graph/Settings/settings.txt")
                                                .Content
                                                .Request()
                                                .GetAsync();

                var settingsString = DeserializeFromStream(settingsStream);
                return JsonConvert.DeserializeObject<SettingsModel>(settingsString);
            }
            catch(Microsoft.Graph.ServiceException ex)
            {
                if (ex.Error.Code.Equals("itemNotFound"))
                {
                    return new SettingsModel();
                }
                Debug.WriteLine("Error get upload file in OneDrive: " + ex.Message);
                throw;
            }
            catch (Exception ex)
            {
                Debug.WriteLine("Error get upload file in OneDrive: " + ex.Message);
                throw;
            }



- Build and run the application.

- Click in Log in button.

- Select **Save App Data in OneDrive** option in menu.

- You see the option you select before selected.
