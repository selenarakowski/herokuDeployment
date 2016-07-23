# How to Deploy a MEAN-Stack Application to Heroku

I have created this tutorial for my activity as an instructor at [DevMountain](https://devmounta.in/).

The goal is to deploy the [favoritePlaces](https://github.com/philippschulte/favoritePlaces) app to [Heroku](https://www.heroku.com/).

To follow along you need to create an account with:

1. [GitHub](https://github.com/)
2. [Heroku](https://www.heroku.com/)
3. [mLab](https://mlab.com/)

Ensure that you have the following installed on your local machine:

* [Node.js](https://nodejs.org/en/)
* [MongoDB](https://www.mongodb.com/)

#### Table of Contents
* [1.0 Generating an SSH key](#one)
* [2.0 Adding a new SSH key to your GitHub account](#two)
* [3.0 Adding a new SSH key to your Heroku account](#three)
* [4.0 Installing Heroku Toolbelt](#four)
* [5.0 Installing favoritePlaces App](#five)
* [6.0 Deploying Your Node App](#six)

## <a name="one"></a>1.0 Generating an SSH key

SSH keys are a way to identify trusted computers without involving passwords.

### 1.1 Checking for existing SSH keys

Before you generate an SSH key, you can check to see if you have any existing SSH keys.

Type the following command in your terminal to see if you already have a public SSH key:

```
$ ls -al ~/.ssh
```

By default, the filenames of the public keys are one of the following:

* id_dsa.pub
* id_ecdsa.pub
* id_ed25519.pub
* id_rsa.pub

If you don't have an existing public and private key pair (for example id_rsa.pub and id_rsa), then you have to generate a new SSH key to connect to [GitHub](https://github.com/) and [Heroku](https://www.heroku.com/).

### 1.2 Deleting existing SSH keys

Type the following command if you want to delete an existing SSH key pair (for example id_rsa.pub and id_rsa):

```
$ rm ~/.ssh/id_rsa
$ rm ~/.ssh/id_rsa.pub
```

If you reprint all the files in that directory by typing:

```
$ ls -al ~/.ssh
```

again, you should see that they are both gone.

### 1.3 Generating a new SSH key

After you've checked for existing SSH keys, you can generate a new SSH key. Paste the text below, substituting in your GitHub email address.

```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

This command creates a new public/private rsa key pair, using the provided email as a label.

In the next step the program will ask you to update the file names:

```
Enter a file in which to save the key (/Users/you/.ssh/id_rsa):
```

**Do not type anything! Just press `Enter`**. This accepts the default file location.

Up next the program will ask you for a secure passphrase:

```
Enter passphrase (empty for no passphrase):
```

Just hit `Enter` and leave this blank!

Then lastly you have to confirm the passphrase:

```
Enter same passphrase again:
```

Just hit `Enter` again to leave it blank again!

And you're good to go! You now have a new SSH key and you can confirm this by rerunning:

```
$ ls -al ~/.ssh
```

## <a name="two"></a>2.0 Adding a new SSH key to your GitHub account

To configure your GitHub account to use your new (or existing) SSH key, you'll also need to add it to your GitHub account.

1. Copy the SSH key to your clipboard  by typing `$ pbcopy < ~/.ssh/id_rsa.pub`
2. Log in to your GitHub account
3. Click your profile photo, then click `Settings`
3. In the user settings sidebar, click `SSH and GPG keys`
4. Click `New SSH key`
5. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal Mac, you might call this key "Personal MacBook Air"
6. Paste your key into the "Key" field
7. Click `Add SSH key`
8. Confirm the action by entering your GitHub password

**.pub is short for "public". This is the version you are allowed to get out. The other `id_rsa` file is the private one and you shouldn't  copy and paste that anywhere!**

## <a name="three"></a>3.0 Adding a new SSH key to your Heroku account

Sign up for `Heroku` for free. `Heroku` has some great tools that make deploying from the command line effortless!

1. Once you have your account you can log back in
2. Go to your `Manage Account` option
3. Scroll down and look for `SSH Keys`
4. Copy and paste your `id_rsa.pub` key
5. Click `Save`

All right, now you have one key registered to `Heroku` but that means you can start running commands from the terminal!

## <a name="four"></a>4.0 Installing Heroku Toolbelt

The Heroku toolbelt will give us access to the Heroku Command Line. Click on the link below to install the Heroku Toolbelt.

[Heroku Toolbelt](https://toolbelt.heroku.com/)

Go ahead and run the instructions for this installer. It'll install a new tool on your computer that lets you create, update, and deploy our apps right from the command line.

Go into your command line and type:

```
$ heroku
```

Now you can see all the commands available to us.

### 4.1 Logging into Heroku

After the installation the only thing you have to do is to login to `Heroku` just once by typing the following command in your terminal:

```
$ heroku login
```

You can confirm that your login went well by running a command like:

```
$ heroku apps
```

Which will return a list of all your apps. In your case you probably won't have anything under my apps but it should still return without an error message!

## <a name="five"></a>5.0 Installing favoritePlaces App

The source code is available on [my GitHub](https://github.com/philippschulte) account, clone it with:

```
$ git clone https://github.com/philippschulte/favoritePlaces.git
```

To prepare your system for running the app locally, run

```
$ npm install
```

and

```
$ bower install
```

in your local directory to install the dependencies.

After all dependencies are installed, you will be ready to run your app locally by typing

```
$ node index
```

or

```
$ npm start
```

## <a name="six"></a>6.0 Deploying Your Node App

The benefit of `Heroku` is that we can deploy from a git repository which makes our lives much easier. Just push and our changes are live!

### 6.1 Create a new app

From within the folder of your git repo, we do the following steps:

1. Create a remote repository (called heroku as opposed to our main origin remote repository) so our application knows where to push our deployable code
2. Push the repository

Let’s create the remote repository:

```
$ heroku create
```

That simple little command creates a brand new `Heroku` app! You can see it automatically generates a kind of weird `url` for your app. If you want to open the app you can run:

```
$ heroku open
```

The command opens a browser with a `Heroku` boilerplate app. This is just a filler and once we push our code you'll see our project at this `url`!

`Heroku` recognizes an app as `Node.js` by the existence of a `package.json` file in the root directory. The `package.json` file determines the version of `Node.js` that will be used to run your application on `Heroku`, as well as the dependencies that should be installed with your application. When an app is deployed, `Heroku` reads this file and installs the appropriate `Node.js` version together with the dependencies using the `npm install` command.

Before we push our project to `Heroku` we run:

```
$ git remote -v
```

and you can see the `origin` remote that was added by `GitHub`. This let's us push and pull changes to our project to `GitHub`. When we ran `$ heroku create`, `Heroku` also added a `remote` were we can push changes to our project and they gonna get live to the web. This is awesome we don't have to leave the `Terminal` in order to update our code in production!

### 6.2 Connecting to existing mLab deployments from Heroku

Sign in to [mLab](https://mlab.com/) and create a new database. Select the `Single-node` plan and the free `Sandbox` standard line.

**Please note that Sandbox databases should not be used in production, as they are intended for development/testing environments that do not require high availability.**

To protect your database, it is best practice to store your database credentials in a `Heroku config variable`. This allows you to avoid hard coding credentials directly in your application code. To store our `MongoDB URI` in a `Heroku config variable` we just have to type:

```
$ heroku config:set MONGODB_URI=mongodb://dbuser:dbpass@ds053312.mongolab.com:53312/dbname
```

Use the `Heroku` config command to get your connection URI by typing:

```
$ heroku config | grep MONGODB_URI
```

You can access this variable in `Node.js` as `process.env.MONGODB_URI`! Make sure that you set the MongoDB connection string equal to:

```javascript
const uri = process.env.MONGOLAB_URI;
```

and reference it when you define your `Mongoose` connection like:

```javascript
mongoose.connect(uri, (err) => {
  console.log(err ? 'Connection to MongoDB failed!' : 'Connected to MongoDB at: ', uri);
});
```

Now our app and database are connected!

### 6.3 Important configuration

Now before we go ahed and push to the `Heroku remote` we have to make sure that:

1. The `port` variable is assigned to Heroku's environment variable so that our app will run probably on the `Heroku` server
2. The command how to start your application is defined in the `package.json` file

`Heroku` actually sets an environment variable and it gives you the `port` you need to listen to! You can access this environment variable by accessing:

```javascript
const port = process.env.PORT || 3000;
```

What we doing here is using the `|| Operator` and what this does is it takes this value and sets it into `port`.  If there is no `process.env.PORT` which there isn't for our local server then it simply uses the `3000` port!

Before we go ahead and do anything else let's rerun our `server` locally by running:

```
$ node index
```

and you can see that our `Express` server started on port `3000`. So it looks like everything is still working well!

Don't forget to update the start command of your app in `package.json`! By default, `Heroku` will look into our `package.json` file under the scripts section and grab `start`. This tells Heroku that when deploying to the web, this command should be used to start our application. Your `package.json` should look similar like the following one:

```json
{
  "name": "your-awesome-app",
  "description": "The best node.js app on the web",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "1.0.0",
    "body-parser": "1.0.0",
    "morgan": "1.0.0",
    "cors": "1.0.0",
    "mongoose": "1.0.0"
  }
}
```

### 6.4 Deploy the code

Now that we have these updates we are actually ready to commit our changes and push it to `Heroku`. Make sure that your working directory is clean by running `$ git status`. If not

1. Add your changes
2. Commit your changes (Commit message could be: "Update port and define start command for Heroku)
3. Push your changes to `GitHub`

Now we are finally ready to push the repository to `Heroku`. When we want to push to `Heroku` it is a little different. To push to `Heroku` we gonna run:

```
$ git push heroku master
```

This informs `git` that we would like to push to the newly create `Heroku` repository and the master branch. If you run this command you can see it pushes it to `Heroku` and we start getting a log file. `Heroku` is actually going ahead and installing our `npm` modules, it is checking out our `package.json` for configurations, and in the end you can see we actually already launched our app. That is honestly all it takes to deploy! You commit your changes and you push them to `Heroku`. Now they are available live on the web.

Ensure that at least one instance of the app is running:

```
$ heroku ps:scale web=1
```

If you remember the crazy random name that `Heroku` generated for you, or renamed the app yourself, go ahead and visit that in browser. There is also a shortcut to open in browser using the command line. Just type:

```
$ heroku open
```

to launch the app in the browser. Now you can see that our app is live on the web. You can go here in any browser on any computer in the world and you gonna see the exact same thing. We no longer running on `localhost` we are actually running on a real web server and it is as easy as pushing to a `git` remote.

One more little bonus! You can actually `rename` your app to whatever you want to call it. To do this run:

```
$ heroku rename new-name-of-your-app
```

and then simply give it a name. It has some rules about spacings and some special characters! If everything works well you can see the `domain` has changed. Just type:

```
$ heroku open
```

to launch your app under the new `url`!
