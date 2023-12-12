## What?

Repo to automate the distribution of [uYouEnhanced](https://github.com/arichorn/uYouEnhanced) to [Firebase App Distribution](https://firebase.google.com/docs/app-distribution) using [fastlane](https://fastlane.tools)

## How?

1. Fork the repo
2. Create a Firebase project and enable App Distribution
3. Create a tester group named "testers"
4. Add an iOS app to the project
5. [Create a Firebase service account](https://console.cloud.google.com/projectselector2/iam-admin/serviceaccounts) with the `Firebase App Distribution Admin` role
6. Create and download a private json key for the service account
7. Create a Standard Class storage bucket for your fastlane certificates and provisioning profiles here: https://console.cloud.google.com/storage/browser
8. Click `Grant Access` on the bucket page and give the `Storage Admin` role to the service account email address you created earlier
9. Create a `.env` file based on `.env.template`, run `source .env`, then run `fastlane match`
10. Create the following repo secrets:
    - `FIREBASE_SERVICE_ACCOUNT_KEY` - Base 64 encoded json key file (`cat key.json | base64 -o output.txt`)
    - `FIREBASE_APP_ID` - The Firebase app ID
    - `GC_BUCKET_NAME` - The name of the storage bucket
    - `BUNDLE_ID` - The bundle ID of the re-signed app

## When?

The action checks for updates every 24 hours and will distribute the latest build if there is a new version

The version check and distribution actions can also be manually triggered