### Introduction

During application development, providing specific authorization flows should be easy with guaranteed security. Open Authorization (OAuth) provides such a standard without having to deal with users' sensitive data such as passwords. 

Firebase implements OAth 2.0 with google auth provider in the most coherent way.


### Prerequisites
To follow along with this tutorial, you will need:
1. Some knowlegde of Vue.js.
2. Node.js 10.x or newer, excluding 13 and 15. These versions are not tested with Quasar.
3. Npm 5.10 or newer / yarn 1.2 or newer.

### Setting up Quasar Vuejs app

Before we setup the app, first check whether Quasar CLI is globally installed on your computer. Using the terminal run:
```bash
$ quasar -v
```
If you get a `command not found`, run the following command to install it.
```bash
$ npm install -g @quasar/cli
```
If you are using yarn, run:
```bash
$ yarn global add @quasar/cli
```

To create a new Quasar app, run the command below.
```
If you are using yarn, run:
```bash
$ yarn global add @quasar/cli
```


### Create a quasar-firebase-app with Quasar
​
To create a new Quasar app, run the command below.
​
```bash
$ quasar create quasar-firebase-app
```
`quasar-firebase-app` is the name of your project.

​
Hit Enter to accept the default project details or edit them to your liking.
​
Using the arrow keys select the first CSS preprocessor:
​
```bash
❯ Sass with SCSS syntax (recommended)
  Sass with indented syntax (recommended)
  Stylus (deprecated)
  None (the others will still be available)
```
Select `Auto-import-in-use Quasar Components` and hit Enter.
​
```bash
? Pick a Quasar components & directives import strategy
❯ * Auto-import in-use Quasar components & directives
    - also treeshakes Quasar; minimum bundle size
  * Import everything from Quasar
    - not treeshaking Quasar; biggest bundle size    
```
​
Then press the spacebar to unselect the ESLint feature, we won't be needing it here. Hit Enter.
​
```bash
❯ (*) ESLint (recommended)
```
<!-- 
Then hit the enter to select the ESLint feature. Hit enter again to select the first preset (Prettier)
```bash
❯ Prettier (https://github.com/prettier/prettier) 
``` -->
Finally, using the arrow keys select yarn. This is what we will use during development, you can use npm if you like.
​
```bash
❯ Yes, use Yarn (recommended)
```

Navigate to the created `quasar-firebase-googleauth` and serve the app by running the commands:
```bash
$ cd quasar-firebase-googleauth
$ quasar dev
```
After serving the app, the URL: http://localhost:8080/#/ opens in your browser to view the app. You'll see Quasar logo and the name "Quasar" at the center of the page.

Open the created `quasar-firebase-googleauth` folder in your editor of choice.

Navigate to `quasar.conf.js` file, go to line 47, change the `vueRouterMode` from `hash` to `history`. This will remove the hash `/#/` from our app URL.

### Creating our app components

Navigate to the `src` folder, open `Index.vue`, delete the whole image tag that looks like below
```html
<img alt="Quasar logo" src="~assets/quasar-logo-full.svg">
```
Rename the `Index.vue` file to `Auth.vue`, create another file named `Home.vue` inside the `pages` folder. Then add a div tag `<div>` inside the template tag with the following code below:
```html
<template>
  <q-page class="flex q-pa-md">
      Welcome Home
    <q-space />
    <div>
      <q-btn
        class="flex flex-center q-px-lg q-py-sm q-mb-md"
        size="md"
        label="Logout"
        @click="logout"
        color="primary"
      />
    </div>
  </q-page>
</template>
```
Inside the `<Script>` tag add the code below:
```javascript
export default {
name: "Home",
  data () {
  return {}
  },
  methods: {
    logout() {
      console.log('logged out')
    }
  }
}
```
Now, navigate to `router` folder, open `routes.js`, edit the routes to match their individual components as below:
```javascript
children: [
     path: '/',
     component: () => import('layouts/MainLayout.vue'),
      { path: '', component: () => import('pages/Auth.vue') },
      { path: '/home', component: () => import('pages/Home.vue'), meta: { requiresAuth:true } }
    ]
```  
According to the routes above, the `/` path is allowed for everyone, but the `/home` is only for signed-in users. This will be well demonstrated after adding firebase to our application.

### Signup/ Signin component
We're going to create a signin/signup component. Navigate to `components` folder create a new file `AuthComponent.vue` and paste the code below:
```html
<template>
  <div>
    <template v-if="tab === 'register'">
      <div class="text-center q-mb-lg">Sign up with</div>
    </template>
    <template v-else>
      <div class="text-center q-mb-lg">Sign in with</div>
    </template>
    <div class="flex flex-center">
      <q-btn class="flex flex-center q-px-lg q-py-sm q-mb-md" color="primary" size="md"  label="Google" 
        @click="google" 
      />
    </div>
    <template v-if="tab === 'register'">
      <p class="text-center">Sign up with credentials</p>
    </template>
    <template v-else>
      <p class="text-center">Sign in with credentials</p>
    </template>

    <q-form @submit="submitForm">
      <q-input outlined class="q-mb-md" type="email" label="Email" v-model="formData.email" />
      <q-input outlined class="q-mb-md" type="password" label="Password" v-model="formData.password" />
      <div class="row">
        <q-space />
        <q-btn type="submit" color="primary" :label="tab" />
      </div>
    </q-form>
    <div class="text-center q-my-md">
      <q-btn flat label="Forgot Password?" color="green" class="text-capitalize rounded-borders"
        v-if="tab !== 'register'" @click="forgotPassword" />
    </div>
    <q-dialog v-model="resetPwdDialog">
      <ForgotPassword />
    </q-dialog>
  </div>
</template>
```    
This is a tab that displays AuthComponent for signing in and signing up. For the `<script>` tag paste the code below:
```javascript
import ForgotPassword from "components/ForgotPassword";
export default {
  name: "AuthComponent",
  props: ['tab'],
  components: { ForgotPassword },
  data (){
    return {
      formData: {
        email: '',
        password: ''
      },
      resetPwdDialog: false
    }
  },
  methods: {
    submitForm () {
      if (this.tab === 'login') {
         this.signInExistingUser(this.formData.email, this.formData.password)
      } else {
        this.createUser(this.formData.email, this.formData.password)
      }
    },
    google () {
      console.log('google login & signup')
    },
     signInExistingUser (email, password) {
      console.log(email, password)
    },
    createUser(email, password) {
      console.log(email, password)
    },
    forgotPassword () {
      this.resetPwdDialog = true
    }
  }
}
```
In the script, we imported the `ForgotPassword` component which we're going to create next. The data function has form input data.

The methods `google()` will handle the firebase google authorization while the `forgotPassword()` alongside `resetPwdDialog` data property will display a dialog for password resets.

### Creating Forgot Password Component  
In this next stage, we're going to create the `ForgotPassword` component, in the `components` folder create `ForgotPassword.vue` file and paste the following code in it.
```html
<template>
  <div class="flex flex-center">
    <q-card style="width: 500px; max-width: 40vw;">
      <q-card-section class="row items-center q-pb-none">
        <div class="text-h6">
          Reset Password
        </div>
        <q-space />
        <q-btn icon="close" flat round dense v-close-popup />
      </q-card-section>
      <q-card-section class="q-pt-md">
        <q-form ref="resetPasswordForm">
          <q-input
            type="email"
            v-model="form.email"
            label="Email *"
            lazy-rules
            :rules="[val => (val && val.length > 0) || 'Please type your email']"
          />
        </q-form>
        <q-card-actions align="right">
          <div class="row q-mt-xs">
            <q-btn
              class="q-pl-md q-pr-md q-mr-md text-capitalize rounded-borders"
              label="Submit"
              color="primary"
              @click="resetPassword"
            />
          </div>
        </q-card-actions>
      </q-card-section>
    </q-card>
  </div>
</template>
```
In the `<script>` tag paste the code below:
```javascript
export default {
  name: "ForgotPassword",
  data (){
    return {
      form: {
        email: ''
      }
    }
  },
  methods: {
    resetPassword () {
      // firebase reset password
    }
  }
}
```
This component is imported to the `AuthComponent.vue` which has a form for password resetting.

By now, everything is not displayed correctly yet. Navigate to the `pages` folder open `Auth.vue ` and paste the code below:

```html
<template>
  <q-page class="flex q-pa-md">
    <q-card class="full-width">
      <q-tabs
        v-model="tab"
        dense
        class="text-grey"
        active-color="primary"
        indicator-color="primary"
        align="justify"
        narrow-indicator
      >
        <q-tab name="login" label="Login" />
        <q-tab name="register" label="Register" />
      </q-tabs>


      <q-tab-panels v-model="tab" animated>
        <q-tab-panel name="login">
          <AuthComponent :tab="tab" />
        </q-tab-panel>

        <q-tab-panel name="register">
          <AuthComponent :tab="tab"/>
        </q-tab-panel>
      </q-tab-panels>
    </q-card>
  </q-page>
</template>
```
The `AuthComponent` above is imported to the `pages/Auth.vue` with props for register and login tabs. In the `<script>` tag paste the following code:
```javascript
import AuthComponent from "components/AuthComponent";
export default {
  components: { AuthComponent },
  data () {
    return {
      tab: 'login'
    }
  }
}
```

### Add Firebase to our application.

To add firebase to our app, ensure the following is done correctly:
1. Visit`[firebase console](https://console.firebase.google.com/u/0/)
2. Click `add project` to create a firebase project to connect to our app. Name it `quasar-google-auth` and click `Continue`
3. Disable Google Analytics for this project and click `Continue` to create our project.
4. After the project is ready click `Continue`. It will take you to the project overview. Click the `web` icon, then register an app name, name it `quasar-firebase-googleauth` and click `Register App`
5. You'll be taken to `step 2 - Add Firebase SDK`, copy the whole script.

We're going to install firebase and create a boot file to initialize firebase before our app runs.
Go back to our project, open the terminal, run the command below:
```bash
yarn add firebase
quasar new boot firebase
```
Navigate to `quasar.conf.js` file, search for `boot` it should be an empty array. Add `firebase.js` boot file in it as indicated below.
```javascript
boot: ['firebase'],
```
Navigate to the `boot` folder, open `firebase.js` file. 

Paste the script you copied the previous step for the firebase SDK. `firebase.js` file structure should resemble the one below.
```javascript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "",
    authDomain: "",
    projectId: "",
    storageBucket: "",
    messagingSenderId: "",
    appId: ""
  };
  firebase.initializeApp(firebaseConfig);

export default firebase
```

### Access Control for Routes
We're going to disable access to routes which requires authorization when a user needs to access them. This is quite easy. Navigate to `routes` folder, open `index.js` file.

`Import firebase from "firebase"` at the top of the file just like we did in the `firebase.js` boot file.
When done, add the following code just above the line `return Router`:
```javascript
  Router.beforeEach(async (to, from, next) => {
    const auth = to.meta.requiresAuth
    if (auth && !await firebase.getCurrentUser()) {
      next('/');
    } else {
      next();
    }
  })
```
Now if the currentUser is null or undefined, we should redirect users to the auth path (`/`). But how do we get currentUser? We can’t use firebase.auth().currentUser because on page refresh that property has not been set yet before the requiresAuth guard is triggered. 

We will have to use the onAuthStateChanged callback somehow. We have to add a method to the firebase object after we initialize the firebase app. The method is added to `firebase.js` boot file. Edit the firebase boot file to resemble the code below.
```javascript
const firebaseConfig = {
    apiKey: "",
    authDomain: "",
    projectId: "",
    storageBucket: "",
    messagingSenderId: "",
    appId: ""
  };
  firebase.initializeApp(firebaseConfig);

  firebase.getCurrentUser = () => {
    return new Promise((resolve, reject) => {
      const unsubscribe = firebase.auth().onAuthStateChanged(user => {
        unsubscribe();
        resolve(user);
      }, reject);
    })
  };
```  

The method after `firebase.initializeApp(firebaseConfig);` will return a Promise which resolves currentUser as soon as it is set. `onAuthStateChanged` will trigger the callback immediately with either null or the user object if signed in. Then we unsubscribe to not listen for further changes.
### Activate SignIn Methods

We need to activate signin methods provided by firebase, we'll activate the `google` and `Email/Password` providers. Go back to the firebase console where we copied the firebase SDK script. click `Continue to console`, it will take you to the project overview.

On the left sidebar click `Authentication`, then click `Set up sign-in method`. Click on `Email/Password` and `Google` providers to activate them. For Email/Password click the first toggle button, don't enable the `passwordless sigin-in` option, while for the Google provider make sure to fill in your `Project support email ` preferably your email address.

Once done, we can get started adding functionalities on our view.

### Adding sign-in with google provider functionality

Navigate to `AuthComponent.vue` file. Let's import firebase. As indicated below,
```javascript
import firebase from "firebase";
``` 
In the `google()` method, we create a provider variable, containing the `GoogleAuthProvider` that's used to signin the user with google. Edit the `google()` method to resemble the code below.
```javascript
    google () {
      const provider = new firebase.auth.GoogleAuthProvider()
      firebase.auth().signInWithPopup(provider)
      .then(result => {
        console.log('result', result)
        this.$q.notify({message: 'Sign In Success.'})
        this.$router.push('/home')
      })
      .catch(error => console.log('error',error))
    },
```
This should be able to sign you in when you click the `Google` signin button.
Before clicking the button, navigate to `quasar.conf.js` file, search for `plugins` this should be an empty array. Add notify plugin, this will provide notification when authentication is done. The plugin should be added as a string. As indicated below
```javascript   
plugins: [ 'Notify' ]
```
After adding the plugin, let's complete the other provider (Email/Password), which comes in handy, when a user does not want to sigin-in with google.

### Adding the Email/Password provider functionality

Open `AuthComponent.vue` file, in the `createUser()` method, this method will be used to create a new user to the database, paste the following code for the method.
```javascript
    createUser(email, password) {
      firebase.auth().createUserWithEmailAndPassword(email, password)
        .then(auth => {
          this.$q.notify({message: 'Sign In Success.'})
          this.$router.push('/home')
        })
        .catch(error => {console.log(error)
        })
    },
```
When a user is created it redirects the user to the home page, with `Sign In Success` notification at the bottom of the page.

Next, we're going to create a `signInExistingUser()` method, this signs in already registered users. Paste the following code for the method.
```javascript
    signInExistingUser (email, password) {
      firebase.auth().signInWithEmailAndPassword(email, password)
        .then((userCredential) => {
          this.$q.notify({message: 'Sign In Success.'})
          this.$router.push('/home')
        })
        .catch(error => { console.log(error)})
    },
```
By now, you can sign-in with google or with email/password. If successful, you are redirected to the home page, containing a welcome message and a logout button.

If you're working locally, and have encountered a problem signing in, go to firebase console in the project, click `Authentication`, then `Sign-in method`, below `Sign-in providers`
you'll see `Authorized domains`. Click `Add domain` and add `localhost`. You can add custom domains when your app is hosted.

Next we're going to add the logout functionality once a user is signed in, they should be able to logout of the app.

### Adding the Logout Functionality

At this stage if you've done everything correctly, you're able to sign-in and get redirected to the home page, where you'll see a logout button.
To add the logout function, navigate to `Pages` folder, open `Home.vue` file, at the beginning of the `<script>` tag `import firebase from "firebase"` just like in `AuthComponent.vue` file

In the method `logout` replace its code to resemble the code below.
```javascript
    logout() {
      firebase.auth().signOut()
      this.$router.push('/')
        .then(() => {
        this.$q.notify({message: 'Sign Out Success.'})
      })
      .catch(error =>  console.log('error',error))
    }
```
This method redirects the user to the auth route and notifies them they've been signed out.

### Adding the Forgot Password Functionality

Incase a user forgets their passwords, they should be able to reset to a new one and interact with our app. Let's take care of that.
Navigate to the `ForgotPassword.vue` file, it has a method `resetPassword` which we added sometime earlier. This method will help us send an email for password resetting.
Paste the following code for the method
```javascript
    resetPassword () {
      firebase.auth().sendPasswordResetEmail(this.form.email)
        .then(() => {
          this.form = {}
          this.$q.notify({message: 'Check you email and reset your password.'})
        })
        .catch(error => { console.log(error)})
    }
```
If a user enters their email and it exists in the database, an email is sent to the user to reset the password. If the email does not exist, an error is thrown.

### Access User Information 

When a user is logged in, we can access information about them and display with a welcome home message. Navigate to the `Home.vue` file. Let's make some few changes.
At the `<template>` tag edit the welcome message to resemble this below
```html
Welcome Home {{ user }} {{ email }}
```  

In the `<script>` tag add two data properties to hold the user's name and email that has signed-in successfully. Edit the data function, to resemble below.
```javascript
data () {
  return {
    user: '',
    email: ''
  }
},
```
Now, lets add a lifecycle hook, when a user is redirected to the home page, we access the user's information and display it to them. Inside the  `<script>` tag just after
the data function paste the hook `created()` below:
```javascript
data () { return { ... }},
created() {
  firebase.auth().onAuthStateChanged((auth) => {
    if (auth) {
      this.user = auth.displayName
      this.email = auth.email
    } else {
      console.log('user name is null')
    }
  })
},
methods: {...}
```      
When a user signs-in either with google or email/password, it will display the welcome message alongside their name and email, or with their email if the username is null. 
### Final component touches

Navigate to the `layouts` folder, open `MainLayout.vue`, delete the following to remove the left side drawer:
1. The whole drawer tag indicated as below.
```html
  <q-drawer>
  ....
  </q-drawer>
```
2. The `EssentialLink.vue` file import just below the opening `<script>` tag. Indicated as below.
```javascript
  import EssentialLink from 'components/EssentialLink.vue
 ```
3. The `components` object in the `script` tag indicated as below.
```javascript
  components: { EssentialLink },
 ```

 ### Conclusion

Firebase implementation of google authentication with standards such as the OAuth 2.0 has proven to be one of the best solutions to providing authentication for applications.

Be it a large or a small scale application, letting a 3rd party application handle your users' sensitive information is reliable, shortens application development time and the 
most important, it enables integration of other social media authentications such as Facebook, Twitter and Github.

This makes new users sign-in to your applications with ease. 
Resulting to more users accessing services your application offers.
 
I have provided [link to the repo](https://github.com/EspiraMarvin/quasar-firebase-googleauth-app)  and  [link to the demo app](https://quasar-firebase-googleauth-app.vercel.app/). That is it.​Happy Coding!