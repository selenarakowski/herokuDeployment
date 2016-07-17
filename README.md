# How to Deploy a Node.js App to Heroku

## 1.0 Generating an SSH key

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

If you don't have an existing public and private key pair (for example id_rsa.pub and id_rsa), then you have to generate a new SSH key to connect to GitHub and Heroku.

### 1.2 Deleting existing SSH keys

Type the following command if you want to delete an existing SSH key pair (for example id_rsa.pub and id_rsa):

```
$ rm ~/.ssh/id_rsa
$ rm ~/.ssh/id_rsa.pub
```

If you reprint all the files in that directory by typing

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

And you're good to go! You now have a new SSH key and you can confirm this by rerunning
```
$ ls -al ~/.ssh
```

## 2.0 Adding a new SSH key to your GitHub account

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
