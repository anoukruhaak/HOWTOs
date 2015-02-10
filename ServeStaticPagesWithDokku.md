#How to serve static pages using Dokku-Alt and Jekyll.

###Who this is for:
If you have a static page that needs serving, like a blog on Jekyll, 
AND you do not want to waste money on Heroku 
AND you are not afraid of the command line, then this HOWTO is for you!


### 1.Create a blog, or promo page using Jekyll. 
It's easy. [Just follow these simple instructions]() and get back here. If you already have a jekyll app, continue to step 2.

### 2. Turn on git 
  ```
  $ cd your-project
  $ git init 
  ```

Now spend lots of time creating the prettiest, awesomest site you can think of. Once you are ready to share it with the world, head back over here.

### 3. Get a server
I personally prefer [Digital Oceans](https://www.digitalocean.com/), but you're obviously free to pick anything else (in which case ignore step 4). 
If you use Digital Oceans, create a droplet in any size you deem appropriate. Just make sure to select Ubuntu 14.04 LTS (or higher). [Also add your ssh key](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-digitalocean-droplets).

### 4. SSH into your droplet:
```
$ ssh root@your-droplet-instance
```

### 5. Install Dokku-Alt on your server:
Dokku-Alt is Dokku on steroids. It's a fork of Dokku, but on top supports awesome things, blablablablablabla
From your server, run: 
```
  $ sudo bash -c "$(curl -fsSL https://raw.githubusercontent.com/dokku-alt/dokku-alt/master/bootstrap.sh)"
```

At the end of the download, you will see a message telling you to finish the configuration at the url mentioned, which is basically: HOSTNAME:PORT, or if you don't have a hostname, ip:port.
Once you finished setup (which is basically just pressing the 'finish setup' button), you are done.

**Tadaah, you now have your own Heroku!** Pretty neat! 
You could deploy pretty much anything from here, but right now we're going to deploy your blog/page!

### 6. Add ssh to your dokku
Run the following command locally, to add your public ssh key to your dokku:
```
cat path/to/publickey | ssh root@ip "sudo sshcommand acl-add dokku [description]"
```
Enter the path to your key and the ip, or hostname. You can change [description] into any **one** word.

### 7. Create a new dokku app
From your server run

```
  dokku create APPNAME
```

### 8. Add a remote to your blog/page
From your blog/page folder:

```
$ git remote add NAME-OF-REMOTE dokku@HOSTNAME:APPNAME
```

### 9. Deploy:
From your project:
```
git push NAME-OF-REMOTE master
```

Or if you want to push from a different branch:

```
git push NAME-OF-REMOTE branch:APPNAME
```

### Not working? 
It happens. You find the logs here: 
```
dokku logs appname
```

Check out which processes are running: 

```
docker ps
```

**If not having a hostname is giving you troubles, let dokku know you don't have a host**:
```
cd /home/dokku/NAMEAPP
touch NO_VHOST
```
