# Firebase SDK for Cloud Functions Quickstart - Cloud Storage trigger

This quickstart demonstrates using **Firebase SDK for Cloud Functions** setup with a Cloud Storage trigger.

## Introduction

This sample automatically generates thumbnails for images that are uploaded to Cloud Storage.


## Functions Code

See file [functions/index.js](functions/index.js) for the thumbnail generation code.

The thumbnail generation is performed using ImageMagick which is installed by default on all Cloud Functions instances. This is a CLI so we execute the command from node using the [child-process-promise](https://www.npmjs.com/package/child-process-promise) package. The image is first downloaded locally from the Cloud Storage bucket to the `tmp` folder using the [google-cloud](https://github.com/GoogleCloudPlatform/google-cloud-node) SDK.

The dependencies are listed in [functions/package.json](functions/package.json).


## Trigger rules

The function triggers on upload of any file to your Firebase project's default Cloud Storage bucket.


## Deploy and test

To deploy and test the sample:

 - Create a Firebase project on the [Firebase Console](https://console.firebase.google.com) and visit the **Storage** tab.
 - Get the code, for instance using `git clone https://github.com/firebase/functions-samples`
 - Enter the correct directory `cd functions-samples/quickstarts/thumbnails`
 - Setup the CLI to use your Firebase project using `firebase use --add` and select your Firebase project
 - Deploy your project's code using `firebase deploy`
 - Go to the Firebase Console **Storage** tab and upload an image. After a short time a thumbnail image with the same name but a `thumb_` prefix will be created in the same folder (make sure you refresh the UI to see the new file).


## Contributing

We'd love that you contribute to the project. Before doing so please read our [Contributor guide](../../CONTRIBUTING.md).


## License

© Google, 2016. Licensed under an [Apache-2](../../LICENSE) license.
