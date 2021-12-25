# Firebase web codelab

> ## Excerpt
>
> In this codelab, you’ll learn how to use the Firebase platform on the web by building a chat app.

---

- On this page
- [Overview](https://firebase.google.com/codelabs/firebase-web#0)
- [Get the sample code](https://firebase.google.com/codelabs/firebase-web#1)
- [Create and set up a Firebase project](https://firebase.google.com/codelabs/firebase-web#2)
- [Install the Firebase command-line interface](https://firebase.google.com/codelabs/firebase-web#3)
- [Run the starter app locally](https://firebase.google.com/codelabs/firebase-web#4)
- [Import and configure Firebase](https://firebase.google.com/codelabs/firebase-web#5)
- [Set up user sign-in](https://firebase.google.com/codelabs/firebase-web#6)
- [Write messages to Cloud Firestore](https://firebase.google.com/codelabs/firebase-web#7)
- [Read messages](https://firebase.google.com/codelabs/firebase-web#8)
- [Send images](https://firebase.google.com/codelabs/firebase-web#9)
- [Show notifications](https://firebase.google.com/codelabs/firebase-web#10)
- [Cloud Firestore security rules](https://firebase.google.com/codelabs/firebase-web#11)
- [Cloud Storage security rules](https://firebase.google.com/codelabs/firebase-web#12)
- [Collect performance data](https://firebase.google.com/codelabs/firebase-web#13)
- [Automatic traces](https://firebase.google.com/codelabs/firebase-web#automatic-traces)
- [Measure first input delay (optional)](https://firebase.google.com/codelabs/firebase-web#measure-first-input-delay-optional)
- [View performance data](https://firebase.google.com/codelabs/firebase-web#view-performance-data)
- [Deploy your app using Firebase Hosting](https://firebase.google.com/codelabs/firebase-web#14)
- [Congratulations!](https://firebase.google.com/codelabs/firebase-web#15)

\_access_time_74 mins remaining

\_access_time_74 mins remaining

## About this codelab

\_subject_Last updated Oct 28, 2021

## [1\. Overview](https://firebase.google.com/codelabs/firebase-web#0)

In this codelab, you'll learn how to use [Firebase](http://firebase.google.com/) to easily create web applications by implementing and deploying a chat client using Firebase products and services.

![3b1284f5144b54f6.png](https://firebase.google.com/codelabs/firebase-web/img/3b1284f5144b54f6.png)

### What you'll learn

- Sync data using Cloud Firestore and Cloud Storage for Firebase.
- Authenticate your users using Firebase Authentication.
- Deploy your web app on Firebase Hosting.
- Send notifications with Firebase Cloud Messaging.
- Collect your web app's performance data.

### What you'll need

- The IDE/text editor of your choice, such as [WebStorm](https://www.jetbrains.com/webstorm), [Atom](https://atom.io/), [Sublime](https://www.sublimetext.com/), or [VS Code](https://code.visualstudio.com/)
- The package manager [npm](https://www.npmjs.com/), which typically comes with [Node.js](https://nodejs.org/en/)
- A terminal/console
- A browser of your choice, such as Chrome
- The codelab's sample code (See the next step of the codelab for how to get the code.)

## [2\. Get the sample code](https://firebase.google.com/codelabs/firebase-web#1)

Clone the codelab's [GitHub repository](https://github.com/firebase/codelab-friendlychat-web) from the command line:

```
git clone https://github.com/firebase/codelab-friendlychat-web
```

Alternatively, if you do not have git installed, you can [download the repository as a ZIP file](https://github.com/firebase/codelab-friendlychat-web/archive/refs/heads/main.zip).

### Import the starter app

Using your IDE, open or import the 📁 `web-start` directory from the cloned repository. This 📁 `web-start` directory contains the starting code for the codelab, which will be a fully functional chat web app.

## [3\. Create and set up a Firebase project](https://firebase.google.com/codelabs/firebase-web#2)

### **Create a Firebase project**

1.  Sign in to [Firebase](https://console.firebase.google.com/).
2.  In the Firebase console, click **Add Project**, and then name your Firebase project **FriendlyChat**. Remember the project ID for your Firebase project.
3.  Uncheck **Enable Google Analytics for this project**
4.  Click **Create Project**.

The application that we're going to build uses Firebase products that are available for web apps:

- **Firebase Authentication** to easily allow your users to sign into your app.
- **Cloud Firestore** to save structured data on the cloud and get instant notification when data changes.
- **Cloud Storage for Firebase** to save files in the cloud.
- **Firebase Hosting** to host and serve your assets.
- **Firebase Cloud Messaging** to send push notifications and display browser popup notifications.
- **Firebase Performance Monitoring** to collect user performance data for your app.

Some of these products need special configuration or need to be enabled using the Firebase console.

### Add a Firebase web app to the project

1.  Click the web icon ![58d6543a156e56f9.png](https://firebase.google.com/codelabs/firebase-web/img/58d6543a156e56f9.png)to create a new Firebase web app.
2.  Register the app with the nickname **Friendly Chat**, then check the box next to **Also set up Firebase Hosting for this app**. Click **Register app**.
3.  On the next step, you'll see a configuration object. Copy just the JS object (not the surrounding HTML) into [firebase-config.js](https://github.com/firebase/friendlychat/blob/master/web/src/firebase-config.js)

![Register web app screenshot](https://firebase.google.com/codelabs/firebase-web/img/register-web-app.png)

### Enable Google **sign-in for Firebase Authentication**

To allow users to sign in to the web app with their Google accounts, we'll use the **Google** sign-in method.

You'll need to enable **Google** sign-in:

1.  In the Firebase console, locate the **Build** section in the left panel.
2.  Click **Authentication**, then click the **Sign-in method** tab (or [click here](https://console.firebase.google.com/project/_/authentication/providers) to go directly there).
3.  Enable the **Google** sign-in provider, then click **Save**.
4.  Set the public-facing name of your app to **Friendly Chat** and choose a **Project support email** from the dropdown menu.
5.  Configure your OAuth consent screen in the [Google Cloud Console](https://console.developers.google.com/apis/credentials/consent) and add a logo:

![d89fb3873b5d36ae.png](https://firebase.google.com/codelabs/firebase-web/img/d89fb3873b5d36ae.png)

### **Enable Cloud Firestore**

The web app uses [Cloud Firestore](https://firebase.google.com/docs/firestore/) to save chat messages and receive new chat messages.

You'll need to enable Cloud Firestore:

1.  In the Firebase console's **Build** section, click **Firestore Database**.
2.  Click **Create database** in the Cloud Firestore pane.

![729991a081e7cd5.png](https://firebase.google.com/codelabs/firebase-web/img/729991a081e7cd5.png)

3.  Select the **Start in test mode** option, then click **Next** after reading the disclaimer about the security rules.

Test mode ensures that we can freely write to the database during development. We'll make our database more secure later on in this codelab.

![77e4986cbeaf9dee.png](https://firebase.google.com/codelabs/firebase-web/img/77e4986cbeaf9dee.png)

4.  Set the location where your Cloud Firestore data is stored. You can leave this as the default or choose a region close to you. Click **Done** to provision Firestore.

![9f2bb0d4e7ca49c7.png](https://firebase.google.com/codelabs/firebase-web/img/9f2bb0d4e7ca49c7.png)

### **Enable Cloud Storage**

The web app uses Cloud Storage for Firebase to store, upload, and share pictures.

You'll need to enable Cloud Storage:

1.  In the Firebase console's **Build** section, click **Storage**.
2.  If there's no **Get Started** button, it means that Cloud storage is already enabled, and you don't need to follow the steps below.
3.  Click **Get Started**.
4.  Read the disclaimer about security rules for your Firebase project, then click **Next**.

With the default security rules, any authenticated user can write anything to Cloud Storage. We'll make our storage more secure later in this codelab.

![62f1afdcd1260127.png](https://firebase.google.com/codelabs/firebase-web/img/62f1afdcd1260127.png)

4.  The Cloud Storage location is preselected with the same region you chose for your Cloud Firestore database. Click **Done** to complete the setup.

![1d7f49ebaddb32fc.png](https://firebase.google.com/codelabs/firebase-web/img/1d7f49ebaddb32fc.png)

## [4\. Install the Firebase command-line interface](https://firebase.google.com/codelabs/firebase-web#3)

The Firebase command-line interface (CLI) allows you to use Firebase Hosting to serve your web app locally, as well as to deploy your web app to your Firebase project.

1.  Install the CLI by running the following npm command:

```
npm -g install firebase-tools
```

2.  Verify that the CLI has been installed correctly by running the following command:

```
firebase --version
```

Make sure that the version of the Firebase CLI is v4.1.0 or later.

3.  Authorize the Firebase CLI by running the following command:

```
firebase login
```

We've set up the web app template to pull your app's configuration for Firebase Hosting from your app's local directory (the repository that you cloned earlier in the codelab). But to pull the configuration, we need to associate your app with your Firebase project.

4.  Make sure that your command line is accessing your app's local `web-start` directory.
5.  Associate your app with your Firebase project by running the following command:

```
firebase use --add
```

6.  When prompted, select your **Project ID**, then give your Firebase project an alias.

An alias is useful if you have multiple environments (production, staging, etc). However, for this codelab, let's just use the alias of `default`.

7.  Follow the remaining instructions on your command line.

## [5\. Run the starter app locally](https://firebase.google.com/codelabs/firebase-web#4)

Now that you have imported and configured your project, you are ready to run the web app for the first time.

1.  In a console from the `web-start` directory, run the following Firebase CLI command:

```
firebase serve --only hosting
```

2.  Your command line should display the following response:

```
✔  hosting: Local server: http://localhost:5000
```

We're using the [Firebase Hosting](https://firebase.google.com/docs/hosting/) emulator to serve our app locally. The web app should now be available from [http://localhost:5000](http://localhost:5000/). All the files that are located under the `public` subdirectory are served.

3.  Using your browser, open your app at [http://localhost:5000](http://localhost:5000/).

You should see your FriendlyChat app's UI, which is not (yet!) functioning:

![4c23f9475228cef4.png](https://firebase.google.com/codelabs/firebase-web/img/4c23f9475228cef4.png)

The app cannot do anything right now, but with your help it will soon! We've only laid out the UI for you so far.

Let's now build a realtime chat!

## [6\. Import and configure Firebase](https://firebase.google.com/codelabs/firebase-web#5)

### **Import the Firebase SDK**

We need to import the Firebase SDK into the app. There are multiple ways to do this as [described in our documentation](https://firebase.google.com/docs/web/setup). For instance, you can import the library from our CDN. Or you can install it locally using npm, then package it in your app if you're using Browserify.

We're going to get the Firebase SDK from npm and use [Webpack](https://webpack.js.org/) to bundle our code. We're doing this so that Webpack can remove any uneccessary code, keeping our JS bundle size small to make sure our app loads as quickly as possible. For this codelab, we've already created a `web-start/package.json` file that includes the Firebase SDK as a dependency, as well as imported the needed functions at the top of `web-start/src/index.js`.

### [package.json](https://github.com/firebase/friendlychat/blob/master/web/package.json)

```
"dependencies": {  "firebase": "^9.0.0"}
```

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js)

```
import { initializeApp } from 'firebase/app';import {  getAuth,  onAuthStateChanged,  GoogleAuthProvider,  signInWithPopup,  signOut,} from 'firebase/auth';import {  getFirestore,  collection,  addDoc,  query,  orderBy,  limit,  onSnapshot,  setDoc,  updateDoc,  doc,  serverTimestamp,} from 'firebase/firestore';import {  getStorage,  ref,  uploadBytesResumable,  getDownloadURL,} from 'firebase/storage';import { getMessaging, getToken, onMessage } from 'firebase/messaging';import { getPerformance } from 'firebase/performance';
```

During this codelab, we're going to use Firebase Authentication, Cloud Firestore, Cloud Storage, Cloud Messaging, and Performance Monitoring, so we're importing all of their libraries. In your future apps, make sure that you're only importing the parts of Firebase that you need, to shorten the load time of your app.

### **Install the Firebase SDK and start your Webpack build**

We need to run a few commands to get our app's build going.

1.  Open a new terminal window
2.  Make sure you're in the `web-start` directory
3.  Run `npm install` to download the Firebase SDK
4.  Run `npm run start` to start up Webpack. Webpack will now continually rebuild our cource code for the rest of the codelab.

### **Configure Firebase**

We also need to configure the Firebase SDK to tell it which Firebase project that we're using.

1.  Go to your [Project settings in the Firebase console](https://console.firebase.google.com/project/_/settings/general/)
2.  In the "Your apps" card, select the nickname of the app for which you need a config object.
3.  Select "Config" from the Firebase SDK snippet pane.
4.  Copy the config object snippet, then add it to `web-start/src/firebase-config.js`.

### [firebase-config.js](https://github.com/firebase/friendlychat/blob/master/web/src/firebase-config.js)

```
const config = {  apiKey: "API_KEY",  authDomain: "PROJECT_ID.firebaseapp.com",  databaseURL: "https://PROJECT_ID.firebaseio.com",  projectId: "PROJECT_ID",  storageBucket: "PROJECT_ID.appspot.com",  messagingSenderId: "SENDER_ID",  appId: "APP_ID",  measurementId: "G-MEASUREMENT_ID",};
```

Now, go to the bottom of `web-start/src/index.js` and initialize Firebase:

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/firebase-config.js)

```
const firebaseAppConfig = getFirebaseConfig();initializeApp(firebaseAppConfig);
```

## [7\. Set up user sign-in](https://firebase.google.com/codelabs/firebase-web#6)

The Firebase SDK should now be ready to use since it's imported and initialized in `index.html`. We're now going to implement user sign-in using [Firebase Authentication](https://firebase.google.com/docs/auth/web/start).

### **Authenticate your users with Google Sign-In**

In the app, when a user clicks the **Sign in with Google** button, the `signIn` function is triggered. (We already set that up for you!) For this codelab, we want to authorize Firebase to use Google as the identity provider. We'll use a popup, but [several other methods](https://firebase.google.com/docs/auth/web/google-signin) are available from Firebase.

1.  In the `web-start` directory, in the subdirectory `src/`, open `index.js`.
2.  Find the function `signIn`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js#L18-L23.js)

```
// Signs-in Friendly Chat.async function signIn() {  // Sign in Firebase using popup auth and Google as the identity provider.  var provider = new GoogleAuthProvider();  await signInWithPopup(getAuth(), provider);}
```

The `signOut` function is triggered when the user clicks the **Sign out** button.

1.  Go back to the file `src/index.js`.
2.  Find the function `signOutUser`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js#L25-L29.js)

```
// Signs-out of Friendly Chat.function signOutUser() {  // Sign out of Firebase.  signOut(getAuth());}
```

### **Track the authentication state**

To update our UI accordingly, we need a way to check if the user is signed in or signed out. With Firebase Authentication, you can register an observer on the authentication state that will be triggered each time the authentication state changes.

1.  Go back to the file `src/index.js`.
2.  Find the function `initFirebaseAuth`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js#L31-L35.js)

```
// Initialize firebase authfunction initFirebaseAuth() {  // Listen to auth state changes.  onAuthStateChanged(getAuth(), authStateObserver);}
```

The code above registers the function `authStateObserver` as the authentication state observer. It will trigger each time the authentication state changes (when the user signs in or signs out). It's at this point that we'll update the UI to display or hide the sign-in button, the sign-out button, the signed-in user's profile picture, and so on. All of these UI parts have already been implemented.

### **Display the information of the signed-in user**

We want to display the signed-in user's profile picture and user name in the top bar of our app. In Firebase, the signed-in user's data is always available in the `currentUser` object. Earlier, we set up the `authStateObserver` function to trigger when the user signs in so that our UI updates accordingly. It will call `getProfilePicUrl` and `getUserName` when triggered.

1.  Go back to the file `src/index.js`.
2.  Find the functions `getProfilePicUrl` and `getUserName`.
3.  Replace both functions with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js#L37-L45.js)

```
// Returns the signed-in user's profile Pic URL.function getProfilePicUrl() {  return getAuth().currentUser.photoURL || '/images/profile_placeholder.png';}// Returns the signed-in user's display name.function getUserName() {  return getAuth().currentUser.displayName;}
```

We display an error message if the user tries to send messages when the user isn't signed in. (You can try it, though!) So, we need to detect if the user is actually signed in.

1.  Go back to the file `src/index.js`.
2.  Find the function `isUserSignedIn`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js#L47-L50.js)

```
// Returns true if a user is signed-in.function isUserSignedIn() {  return !!getAuth().currentUser;}
```

### Test signing in to the app

1.  If your app is still being served, refresh your app in the browser. Otherwise, run `firebase serve --only hosting` on the command line to start serving the app from [http://localhost:5000](http://localhost:5000/), and then open it in your browser.
2.  Sign in to the app using the sign-in button and your Google account. If you see an error message stating `auth/operation-not-allowed`, check to make sure that you enabled Google Sign-in as an authentication provider in the Firebase console.
3.  After signing in, your profile picture and user name should be displayed: ![c7401b3d44d0d78b.png](https://firebase.google.com/codelabs/firebase-web/img/c7401b3d44d0d78b.png)

## [8\. Write messages to Cloud Firestore](https://firebase.google.com/codelabs/firebase-web#7)

In this section, we'll write some data to Cloud Firestore so that we can populate the app's UI. This can be done manually with the [Firebase console](https://console.firebase.google.com/), but we'll do it in the app itself to demonstrate a basic Cloud Firestore write.

### **Data model**

Cloud Firestore data is split into collections, documents, fields, and subcollections. We will store each message of the chat as a document in a top-level collection called `messages`.

![688d7bc5fb662b57.png](https://firebase.google.com/codelabs/firebase-web/img/688d7bc5fb662b57.png)

### **Add messages to Cloud Firestore**

To store the chat messages that are written by users, we'll use [Cloud Firestore](https://firebase.google.com/docs/firestore/).

In this section, you'll add the functionality for users to write new messages to your database. A user clicking the **SEND** button will trigger the code snippet below. It adds a message object with the contents of the message fields to your Cloud Firestore instance in the `messages` collection. The `add()` method adds a new document with an automatically generated ID to the collection.

1.  Go back to the file `src/index.js`.
2.  Find the function `saveMessage`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js#L52-L63)

```
// Saves a new message to Cloud Firestore.async function saveMessage(messageText) {  // Add a new message entry to the Firebase database.  try {    await addDoc(collection(getFirestore(), 'messages'), {      name: getUserName(),      text: messageText,      profilePicUrl: getProfilePicUrl(),      timestamp: serverTimestamp()    });  }  catch(error) {    console.error('Error writing new message to Firebase Database', error);  }}
```

### **Test sending messages**

1.  If your app is still being served, refresh your app in the browser. Otherwise, run `firebase serve --only hosting` on the command line to start serving the app from [http://localhost:5000](http://localhost:5000/), and then open it in your browser.
2.  After signing in, enter a message such as "Hey there!", and then click **SEND**. This will write the message into Cloud Firestore. However, _you won't yet see the data in your actual web app_ because we still need to implement _retrieving_ the data (the next section of the codelab).
3.  You can see the newly added message in your Firebase Console. Open your Firebase Console. Under the **Build** section click **Firestore Database** (or click [here](https://console.firebase.google.com/project/_/firestore/data) and select your project) and you should see the **messages** collection with your newly added message:

![6812efe7da395692.png](https://firebase.google.com/codelabs/firebase-web/img/6812efe7da395692.png)

## [9\. Read messages](https://firebase.google.com/codelabs/firebase-web#8)

### Synchronize **messages**

To read messages in the app, we'll need to add listeners that trigger when data changes and then create a UI element that shows new messages.

We'll add code that listens for newly added messages from the app. In this code, we'll register the listener that listens for changes made to the data. We'll only display the last 12 messages of the chat to avoid displaying a very long history upon loading.

1.  Go back to the file `src/index.js`.
2.  Find the function `loadMessages`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js#L52-L63)

```
// Loads chat messages history and listens for upcoming ones.function loadMessages() {  // Create the query to load the last 12 messages and listen for new ones.  const recentMessagesQuery = query(collection(getFirestore(), 'messages'), orderBy('timestamp', 'desc'), limit(12));// Start listening to the query.  onSnapshot(recentMessagesQuery, function(snapshot) {    snapshot.docChanges().forEach(function(change) {      if (change.type === 'removed') {        deleteMessage(change.doc.id);      } else {        var message = change.doc.data();        displayMessage(change.doc.id, message.timestamp, message.name,                      message.text, message.profilePicUrl, message.imageUrl);      }    });  });}
```

To listen to messages in the database, we create a query on a collection by using the `collection` function to specify which collection the data that we want to listen to is in. In the code above, we're listening to the changes within the `messages` collection, which is where the chat messages are stored. We're also applying a limit by only listening to the last 12 messages using `.limit(12)` and ordering the messages by date using `orderBy('timestamp', 'desc')` to get the 12 newest messages.

The `onSnapshot` function takes a query as its first parameter, and a callback function as its second. The callback function will be triggered when there are any changes to documents that match the query. This could be if a message gets deleted, modified, or added. You can read more about this in the [Cloud Firestore documentation](https://firebase.google.com/docs/firestore/query-data/listen).

### Test synchronizing messages

1.  If your app is still being served, refresh your app in the browser. Otherwise, run `firebase serve --only hosting` on the command line to start serving the app from [http://localhost:5000](http://localhost:5000/), and then open it in your browser.
2.  The messages that you created earlier into the database should be displayed in the FriendlyChat UI (see below). Feel free to write new messages; they should appear instantly.
3.  _(Optional)_ You can try manually deleting, modifying, or adding new messages directly in the **Database** section of the Firebase console; any changes should be reflected in the UI.

Congratulations! You are reading Cloud Firestore documents in your app!

![2168dec79b573d07.png](https://firebase.google.com/codelabs/firebase-web/img/2168dec79b573d07.png)

## [10\. Send images](https://firebase.google.com/codelabs/firebase-web#9)

We'll now add a feature that shares images.

While Cloud Firestore is good for storing structured data, Cloud Storage is better suited for storing files. [Cloud Storage for Firebase](https://firebase.google.com/docs/storage/) is a file/blob storage service, and we'll use it to store any images that a user shares using our app.

### Save images to Cloud Storage

For this codelab, we've already added for you a button that triggers a file picker dialog. After selecting a file, the `saveImageMessage` function is called, and you can get a reference to the selected file. The `saveImageMessage` function accomplishes the following:

1.  Creates a "placeholder" chat message in the chat feed, so that users see a "Loading" animation while we upload the image.
2.  Uploads the image file to Cloud Storage to this path: `/<uid>/<messageId>/<file_name>`
3.  Generates a publicly readable URL for the image file.
4.  Updates the chat message with the newly uploaded image file's URL in lieu of the temporary loading image.

Now you'll add the functionality to send an image:

1.  Go back to the file `src/index.js`.
2.  Find the function `saveImageMessage`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/src/index.js#L84-109)

```
// Saves a new message containing an image in Firebase.// This first saves the image in Firebase storage.async function saveImageMessage(file) {  try {    // 1 - We add a message with a loading icon that will get updated with the shared image.    const messageRef = await addDoc(collection(getFirestore(), 'messages'), {      name: getUserName(),      imageUrl: LOADING_IMAGE_URL,      profilePicUrl: getProfilePicUrl(),      timestamp: serverTimestamp()    });// 2 - Upload the image to Cloud Storage.    const filePath = `${getAuth().currentUser.uid}/${messageRef.id}/${file.name}`;    const newImageRef = ref(getStorage(), filePath);    const fileSnapshot = await uploadBytesResumable(newImageRef, file);// 3 - Generate a public URL for the file.    const publicImageUrl = await getDownloadURL(newImageRef);// 4 - Update the chat message placeholder with the image's URL.    await updateDoc(messageRef,{      imageUrl: publicImageUrl,      storageUri: fileSnapshot.metadata.fullPath    });  } catch (error) {    console.error('There was an error uploading a file to Cloud Storage:', error);  }}
```

### **Test sending images**

1.  If your app is still being served, refresh your app in the browser. Otherwise, run `firebase serve --only hosting` on the command line to start serving the app from [http://localhost:5000](http://localhost:5000/), and then open it in your browser.
2.  After signing in, click the image upload button ![13734cb66773e5a3.png](https://firebase.google.com/codelabs/firebase-web/img/13734cb66773e5a3.png) and select an image file using the file picker. If you're looking for an image, feel free to use this [nice picture of a coffee cup](https://www.pexels.com/photo/aroma-aromatic-art-artistic-434213/).
3.  A new message should appear in the app's UI with your selected image: ![3b1284f5144b54f6.png](https://firebase.google.com/codelabs/firebase-web/img/3b1284f5144b54f6.png)

If you try adding an image while not signed in, you should see a Toast notification telling you that you must sign in to add images.

## [11\. Show notifications](https://firebase.google.com/codelabs/firebase-web#10)

We'll now add support for browser notifications. The app will notify users when new messages are posted in the chat. [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/) (FCM) is a cross-platform messaging solution that lets you reliably deliver messages and notifications at no cost.

### **Add the FCM service worker**

The web app needs a [service worker](https://developer.mozilla.org/en/docs/Web/API/Service_Worker_API) that will receive and display web notifications.

1.  From the `web-start` directory, in the `src` directory, open `firebase-messaging-sw.js`.
2.  Add the following content to that file.

### [firebase-messaging-sw.js](https://github.com/firebase/friendlychat/blob/master/web/src/firebase-messaging-sw.js)

```
// Import and configure the Firebase SDKimport { initializeApp } from 'firebase/app';import { getMessaging } from 'firebase/messaging/sw';import { getFirebaseConfig } from './firebase-config';const firebaseApp = initializeApp(getFirebaseConfig());getMessaging(firebaseApp);console.info('Firebase messaging service worker is set up');
```

The service worker simply needs to load and initialize the Firebase Cloud Messaging SDK, which will take care of displaying notifications.

### **Get FCM device tokens**

When notifications have been enabled on a device or browser, you'll be given a **device token**. This device token is what we use to send a notification to a particular device or particular browser.

When the user signs-in, we call the `saveMessagingDeviceToken` function. That's where we'll get the **FCM device token** from the browser and save it to Cloud Firestore.

1.  Go back to the file `src/index.js`.
2.  Find the function `saveMessagingDeviceToken`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/public/src/index.js)

```
// Saves the messaging device token to Cloud Firestore.async function saveMessagingDeviceToken() {  try {    const currentToken = await getToken(getMessaging());    if (currentToken) {      console.log('Got FCM device token:', currentToken);      // Saving the Device Token to Cloud Firestore.      const tokenRef = doc(getFirestore(), 'fcmTokens', currentToken);      await setDoc(tokenRef, { uid: getAuth().currentUser.uid });// This will fire when a message is received while the app is in the foreground.      // When the app is in the background, firebase-messaging-sw.js will receive the message instead.      onMessage(getMessaging(), (message) => {        console.log(          'New foreground notification from Firebase Messaging!',          message.notification        );      });    } else {      // Need to request permissions to show notifications.      requestNotificationsPermissions();    }  } catch(error) {    console.error('Unable to get messaging token.', error);  };}
```

However, this code won't work initially. For your app to be able to retrieve the device token, the user needs to grant your app permission to show notifications (next step of the codelab).

### **Request permissions to show notifications**

When the user has not yet granted your app permission to show notifications, you won't be given a device token. In this case, we call the `firebase.messaging().requestPermission()` method, which will display a browser dialog asking for this permission ( [in supported browsers](https://caniuse.com/#feat=push-api)).

![8b9d0c66dc36153d.png](https://firebase.google.com/codelabs/firebase-web/img/8b9d0c66dc36153d.png)

1.  Go back to the file `src/index.js`.
2.  Find the function `requestNotificationsPermissions`.
3.  Replace the entire function with the following code.

### [index.js](https://github.com/firebase/friendlychat/blob/master/web/public/src/index.js)

```
// Requests permissions to show notifications.async function requestNotificationsPermissions() {  console.log('Requesting notifications permission...');  const permission = await Notification.requestPermission();if (permission === 'granted') {    console.log('Notification permission granted.');    // Notification permission granted.    await saveMessagingDeviceToken();  } else {    console.log('Unable to get permission to notify.');  }}
```

### **Get your device token**

1.  If your app is still being served, refresh your app in the browser. Otherwise, run `firebase serve --only hosting` on the command line to start serving the app from [http://localhost:5000](http://localhost:5000/), and then open it in your browser.
2.  After signing in, the notifications permission dialog should appear: ![bd3454e6dbfb6723.png](https://firebase.google.com/codelabs/firebase-web/img/bd3454e6dbfb6723.png)
3.  Click **Allow**.
4.  Open the JavaScript console of your browser. You should see the following message: `Got FCM device token: cWL6w:APA91bHP...4jDPL_A-wPP06GJp1OuekTaTZI5K2Tu`
5.  Copy your device token. You'll need it for the next stage of the codelab.

### **Send a notification to your device**

Now that you have your device token, you can send a notification.

1.  Open the [Cloud Messaging tab of the Firebase console](https://console.firebase.google.com/project/_/notification).
2.  Click "New Notification"
3.  Enter a notification title and notification text.
4.  On the right side of the screen, click "send a test message"
5.  Enter the device token you copied from the JavaScript console of your browser, then click the plus ("+") sign
6.  Click "test"

If your app is in the foreground, you'll see the notification in the JavaScript console.

If your app is in the background, a notification should appear in your browser, as in this example:

![de79e8638a45864c.png](https://firebase.google.com/codelabs/firebase-web/img/de79e8638a45864c.png)

## [12\. Cloud Firestore security rules](https://firebase.google.com/codelabs/firebase-web#11)

### View **database security rules**

Cloud Firestore uses a specific [rules language](https://firebase.google.com/docs/firestore/security/overview) to define access rights, security, and data validations.

When setting up the Firebase project at the beginning of this codelab, we chose to use "Test mode" default security rules so that we didn't restrict access to the datastore. In the [Firebase console](https://console.firebase.google.com/), in the **Database** section's **Rules** tab, you can view and modify these rules.

Right now, you should see the default rules, which do not restrict access to the datastore. This means that any user can read and write to any collections in your datastore.

```
rules_version = '2';service cloud.firestore {  match /databases/{database}/documents {    match /{document=**} {      allow read, write;    }  }}
```

We'll update the rules to restrict things by using the following rules:

### [firestore.rules](https://github.com/firebase/friendlychat/blob/master/web/firestore.rules)

```
rules_version = '2';service cloud.firestore {  match /databases/{database}/documents {    // Messages:    //   - Anyone can read.    //   - Authenticated users can add and edit messages.    //   - Validation: Check name is same as auth token and text length below 300 char or that imageUrl is a URL.    //   - Deletes are not allowed.    match /messages/{messageId} {      allow read;      allow create, update: if request.auth != null                    && request.resource.data.name == request.auth.token.name                    && (request.resource.data.text is string                      && request.resource.data.text.size() <= 300                      || request.resource.data.imageUrl is string                      && request.resource.data.imageUrl.matches('https?://.*'));      allow delete: if false;    }    // FCM Tokens:    //   - Anyone can write their token.    //   - Reading list of tokens is not allowed.    match /fcmTokens/{token} {      allow read: if false;      allow write;    }  }}
```

### **Update database security rules**

There are two ways to edit your database security rules, either in the Firebase console or from a local rules file deployed using the Firebase CLI.

To update security rules in the Firebase console:

1.  Go to the **Database** section from the left panel, and then click the **Rules** tab.
2.  Replace the default rules that are already in the console with the rules shown above.
3.  Click **Publish**.

To update security rules from a local file:

1.  From the `web-start` directory, open `firestore.rules`.
2.  Replace the default rules that are already in the file with the rules shown above.
3.  From the `web-start` directory, open `firebase.json`.
4.  Add the `firestore.rules` attribute pointing to `firestore.rules`, as shown below. (The `hosting` attribute should already be in the file.)

### [firebase.json](https://github.com/firebase/friendlychat/blob/master/web/firebase.json#L2-L4.json)

```
{  // Add this!  "firestore": {    "rules": "firestore.rules"  },  "hosting": {    "public": "./public"  }}
```

5.  Deploy the security rules using the Firebase CLI by running the following command:

```
firebase deploy --only firestore
```

6.  Your command line should display the following response:

```
=== Deploying to 'friendlychat-1234'...i  deploying firestorei  firestore: checking firestore.rules for compilation errors...✔  firestore: rules file firestore.rules compiled successfullyi  firestore: uploading rules firestore.rules...✔  firestore: released rules firestore.rules to cloud.firestore✔  Deploy complete!Project Console: https://console.firebase.google.com/project/friendlychat-1234/overview
```

## [13\. Cloud Storage security rules](https://firebase.google.com/codelabs/firebase-web#12)

### **View Cloud Storage security rules**

Cloud Storage for Firebase uses a specific [rules language](https://firebase.google.com/docs/storage/security/start) to define access rights, security, and data validations.

When setting up the Firebase project at the beginning of this codelab, we chose to use the default Cloud Storage security rule that only allows authenticated users to use Cloud Storage. In the [Firebase console](https://console.firebase.google.com/), in the **Storage** section's **Rules** tab, you can view and modify rules. You should see the default rule which allows any signed-in user to read and write any files in your storage bucket.

```
rules_version = '2';service firebase.storage {  match /b/{bucket}/o {    match /{allPaths=**} {      allow read, write: if request.auth != null;    }  }}
```

We'll update the rules to do the following:

- Allow each user to write only to their own specific folders
- Allow anyone to read from Cloud Storage
- Make sure that the files uploaded are images
- Restrict the size of the images that can be uploaded to maximum 5 MB

This can be implemented using the following rules:

### [storage.rules](https://github.com/firebase/friendlychat/blob/master/web/storage.rules)

```
rules_version = '2';// Returns true if the uploaded file is an image and its size is below the given number of MB.function isImageBelowMaxSize(maxSizeMB) {  return request.resource.size < maxSizeMB * 1024 * 1024      && request.resource.contentType.matches('image/.*');}service firebase.storage {  match /b/{bucket}/o {    match /{userId}/{messageId}/{fileName} {      allow write: if request.auth != null && request.auth.uid == userId && isImageBelowMaxSize(5);      allow read;    }  }}
```

### **Update Cloud Storage security rules**

There are two ways to edit your storage security rules: either in the Firebase console or from a local rules file deployed using the Firebase CLI.

To update security rules in the Firebase console:

1.  Go to the **Storage** section from the left panel, and then click the **Rules** tab.
2.  Replace the default rule that is already in the console with the rules shown above.
3.  Click **Publish**.

To update security rules from a local file:

1.  From the `web-start` directory, open `storage.rules`.
2.  Replace the default rules that are already in the file with the rules shown above.
3.  From the `web-start` directory, open `firebase.json`.
4.  Add the `storage.rules` attribute pointing to the `storage.rules` file, as shown below. (The `hosting` and `database` attribute should already be in the file.)

### [firebase.json](https://github.com/firebase/friendlychat/blob/master/web/firebase.json#L5-L7.json)

```
{  // If you went through the "Cloud Firestore Security Rules" step.  "firestore": {    "rules": "firestore.rules"  },  // Add this!  "storage": {    "rules": "storage.rules"  },  "hosting": {    "public": "./public"  }}
```

6.  Deploy the security rules using the Firebase CLI by running the following command:

```
firebase deploy --only storage
```

7.  Your command line should display the following response:

```
=== Deploying to 'friendlychat-1234'...i  deploying storagei  storage: checking storage.rules for compilation errors...✔  storage: rules file storage.rules compiled successfullyi  storage: uploading rules storage.rules...✔  storage: released rules storage.rules to firebase.storage/friendlychat-1234.appspot.com✔  Deploy complete!Project Console: https://console.firebase.google.com/project/friendlychat-1234/overview
```

## [14\. Collect performance data](https://firebase.google.com/codelabs/firebase-web#13)

You can use the Performance Monitoring SDK to collect real-world performance data from your app and then review and analyze that data in the Firebase console. Performance Monitoring helps you to understand where and when the performance of your app can be improved so that you can use that information to fix performance issues.

There are various ways to integrate with the Firebase Performance Monitoring JavaScript SDK. In this codelab, we enabled Performance Monitoring from **Hosting URLs**. Refer to the [documentation](https://firebase.google.com/docs/perf-mon/get-started-web) to see other methods of enabling the SDK.

## Automatic traces

Since we already import `getPerformance` at the top of `web-start/src/index.js`, we just need to add one line to tell Performance Monitoring to automatically collect page load and network request metrics for you when users visit your deployed site!

1.  In `web-start/src/index.js`, add the following line below the existing `TODO` to initialize Performance Monitoring.

### [index.js](https://github.com/firebase/friendlychat-web/blob/master/web/src/index.js#L386-L387)

```
// TODO: Enable Firebase Performance Monitoring.getPerformance();
```

## **Measure first input delay (optional)**

[First input delay](https://developers.google.com/web/updates/2018/05/first-input-delay) is useful since the browser responding to a user interaction gives your users their first impressions about the responsiveness of your app.

First input delay starts when the user first interacts with an element on the page, like clicking a button or hyperlink. It stops immediately after the browser is able to respond to the input, meaning that the browser isn't busy loading or parsing your page's content.

If you'd like to measure first input delay, you'll need to include the following code directly.

1.  Open `public/index.html`.
2.  Uncomment the `script` tag on the following line.

[**index.html**](https://github.com/firebase/friendlychat-web/blob/master/web/public/index.html#L52-L53)

```
<!-- TODO: Enable First Input Delay polyfill library. --><script type="text/javascript">!function(n,e){var t,o,i,c=[],f={passive:!0,capture:!0},r=new Date,a="pointerup",u="pointercancel";function p(n,c){t||(t=c,o=n,i=new Date,w(e),s())}function s(){o>=0&&o<i-r&&(c.forEach(function(n){n(o,t)}),c=[])}function l(t){if(t.cancelable){var o=(t.timeStamp>1e12?new Date:performance.now())-t.timeStamp;"pointerdown"==t.type?function(t,o){function i(){p(t,o),r()}function c(){r()}function r(){e(a,i,f),e(u,c,f)}n(a,i,f),n(u,c,f)}(o,t):p(o,t)}}function w(n){["click","mousedown","keydown","touchstart","pointerdown"].forEach(function(e){n(e,l,f)})}w(n),self.perfMetrics=self.perfMetrics||{},self.perfMetrics.onFirstInputDelay=function(n){c.push(n),s()}}(addEventListener,removeEventListener);</script>
```

To read more about the first input delay polyfill, take a look at the [documentation](https://firebase.google.com/docs/perf-mon/get-started-web#add-first-input-delay-polyfill).

## **View performance data**

Since you haven't deployed your site yet (you'll deploy it in the next step), here's a screenshot showing the metrics about page load performance that you'll see in the Firebase console within 30 minutes of users interacting with your deployed site:

![29389131150f33d7.png](https://firebase.google.com/codelabs/firebase-web/img/29389131150f33d7.png)

When you integrate the Performance Monitoring SDK into your app, you don't need to write any other code before your app starts automatically monitoring several critical aspects of performance. For web apps, the SDK logs aspects like first contentful paint, ability for users to interact with your app, and more.

You can also set up custom traces, metrics, and attributes to measure specific aspects of your app. Visit the documentation to learn more about [custom traces and metrics](https://firebase.google.com/docs/perf-mon/get-started-web#add-custom-trace) and [custom attributes](https://firebase.google.com/docs/perf-mon/custom-attributes).

## [15\. Deploy your app using Firebase Hosting](https://firebase.google.com/codelabs/firebase-web#14)

Firebase offers a [hosting service](https://firebase.google.com/docs/hosting/) to serve your assets and web apps. You can deploy your files to Firebase Hosting using the Firebase CLI. Before deploying, you need to specify in your `firebase.json` file which local files should be deployed. For this codelab, we've already done this for you because this step was required to serve our files during this codelab. The hosting settings are specified under the `hosting` attribute:

### [firebase.json](https://github.com/firebase/friendlychat/blob/master/web/firebase.json#L8-L17)

```
{  // If you went through the "Cloud Firestore Security Rules" step.  "firestore": {    "rules": "firestore.rules"  },  // If you went through the "Storage Security Rules" step.  "storage": {    "rules": "storage.rules"  },  "hosting": {    "public": "./public"  }}
```

These settings tell the CLI that we want to deploy all files in the `./public` directory ( `"public": "./public"` ).

1.  Make sure that your command line is accessing your app's local `web-start` directory.
2.  Deploy your files to your Firebase project by running the following command:

```
firebase deploy --except functions
```

3.  The console should display the following:

```
=== Deploying to 'friendlychat-1234'...i  deploying firestore, storage, hostingi  storage: checking storage.rules for compilation errors...✔  storage: rules file storage.rules compiled successfullyi  firestore: checking firestore.rules for compilation errors...✔  firestore: rules file firestore.rules compiled successfullyi  storage: uploading rules storage.rules...i  firestore: uploading rules firestore.rules...i  hosting[friendlychat-1234]: beginning deploy...i  hosting[friendlychat-1234]: found 8 files in ./public✔  hosting[friendlychat-1234]: file upload complete✔  storage: released rules storage.rules to firebase.storage/friendlychat-1234.appspot.com✔  firestore: released rules firestore.rules to cloud.firestorei  hosting[friendlychat-1234]: finalizing version...✔  hosting[friendlychat-1234]: version finalizedi  hosting[friendlychat-1234]: releasing new version...✔  hosting[friendlychat-1234]: release complete✔  Deploy complete!Project Console: https://console.firebase.google.com/project/friendlychat-1234/overviewHosting URL: https://friendlychat-1234.firebaseapp.com
```

4.  Visit your web app that's now fully hosted on a global CDN using Firebase Hosting at two of your very own Firebase subdomains:

- `https://<firebase-projectId>.firebaseapp.com`
- `https://<firebase-projectId>.web.app`

Alternatively, you can run `firebase open hosting:site` in the command line.

Visit the documentation to learn more about [how Firebase Hosting works](https://firebase.google.com/docs/hosting/#how_does_it_work).

Go to your project's Firebase console **Hosting** section to view useful hosting information and tools, including the history of your deploys, the functionality to roll back to previous versions of your app, and the workflow to set up a custom domain.

## [16\. Congratulations!](https://firebase.google.com/codelabs/firebase-web#15)

You've used Firebase to build a real-time chat web application!

### **What we've covered**

- Firebase Authentication
- Cloud Firestore
- Firebase SDK for Cloud Storage
- Firebase Cloud Messaging
- Firebase Performance Monitoring
- Firebase Hosting

### Next steps

### **Learn more**

- [firebase.google.com](https://firebase.google.com/)

Except as otherwise noted, the content of this page is licensed under the [Creative Commons Attribution 4.0 License](https://creativecommons.org/licenses/by/4.0/), and code samples are licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0). For details, see the [Google Developers Site Policies](https://developers.google.com/site-policies). Java is a registered trademark of Oracle and/or its affiliates.
