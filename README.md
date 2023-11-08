## What?

Repo to automate the distribution of [uYouPlusExtra](https://github.com/arichorn/uYouPlusExtra) to [Firebase App Distribution](https://firebase.google.com/docs/app-distribution) using [fastlane](https://fastlane.tools)

The action checks for updates every 24 hours and will distribute the latest build if there is a new version

## How?
1. Fork the repo
2. Create a Firebase project and enable App Distribution
3. Add an iOS app to the project
4. [Create a Firebase service account](https://console.cloud.google.com/projectselector2/iam-admin/serviceaccounts) with the `Firebase App Distribution Admin` role
5. Create and download a private json key for the service account
6. Create a Standard Class storage bucket for your fastlane certificates and provisioning profiles here: https://console.cloud.google.com/storage/browser
7. Click `Grant Access` on the bucket page and give the `Storage Admin` role to the service account email address you created earlier
8. Add `team_id("your_team_id")` to the `Matchfile` (the CLI selector is bugged) and run `fastlane match`
9. Create the following repo secrets:
   1. `FIREBASE_SERVICE_ACCOUNT_KEY` - The contents of the json key file
   2. `FIREBASE_APP_ID` - The Firebase app ID
   3. `GC_BUCKET_NAME` - The name of the storage bucket
   4. `BUNDLE_ID` - The bundle ID of the re-signed app