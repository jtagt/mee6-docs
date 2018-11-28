# Getting a YouTube API Key

Getting a YouTube API key is a long enough part of the installation that it merits its own guide. All you need is a Google Account.

1. Navigate to `https://console.cloud.google.com`, and a popup should appear.
2. In the popup, you can choose whether to be added to the mailing list (it will email the email address associated with your account), but you *must* accept the Terms of Service, or ToS. You can read it by following the blue link `Terms of Service`. Once the proper options are selected, click `AGREE AND CONTINUE`.
3. Welcome to Google Cloud Platform! Press `Select a Project` (near top left), and press the **+** button in the top right of the resulting popup. Name your project someting you'll remember ("MEE6 Selfhost", maybe?). Then, press the `Create` button, and you have a project!
5. You should be back on the main screen. Click `Select a Project`, but this time, select your new project instead of creating a new one.
6. You have a new project selected and ready! Click the three horizontal bars in the top left, and mouse over `APIs and Services`. Select the resulting `Dashboard` option. Ensure that where it said `Select a Project` three steps ago, it now reads the name of your project. If it doesn't, try selecting your project again, as in Step 5.
7. Now, mouse over the pixelated `API` text on the left edge, and select `Library`. Scroll down and select `YouTube Data API v3`, and press `Enable`. It should take some time to load.
8. Near the top of the screen there should be a warning: `To use this API, you may need credentials. Click 'Create credentials' to get started.` To the right of this should be a matching `Create Credentials` button. Click it.
9. The first option, `Which API are you using?` is fine as it is. Set the next option, `Where will you be calling the API from?`, to `Web Server`. The last option, `What data will you be accessing?`, should be set to `Public Data`.
10. Press the blue `What credentials do I need?`, and there it is! An API key! ~~Grab it before you computer explodes~~. 