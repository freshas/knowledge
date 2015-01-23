
## Step 1: Install rbenv

Before we do anything else, we should run a quick update to make sure that all of the packages we download to our virtual server are up to date:

```
apt-get update
apt-get upgrade
```

Once you update the system and the apt repositories you are able to install the desired rbenv. You need to first install some dependencies:

```
apt-get -y install build-essential git-core zlib1g-dev libssl-dev libreadline6-dev
```

After installing the dependencies clone the Github repo of rbenv into `/usr/local/rbenv` and install it system-wide by running the following commands:

```
git clone git://github.com/sstephenson/rbenv.git /usr/local/rbenv

echo 'export RBENV_ROOT=/usr/local/rbenv' > /etc/profile.d/rbenv.sh
echo 'export PATH=$RBENV_ROOT/bin:$PATH' >> /etc/profile.d/rbenv.sh
echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh
ln -s /usr/local/rbenv/completions/rbenv.bash /etc/bash_completion.d/rbenv
 
source /etc/profile.d/rbenv.sh
```

Now rbenv is install system-wide on the server you are on now. Install ruby-build for installing Ruby versions via rbenv using these commands:
 ```
git clone git://github.com/sstephenson/ruby-build.git /tmp/ruby-build
cd /tmp/ruby-build
PREFIX=/usr/local/rbenv ./install.sh
cd ..
rm -rf /tmp/ruby-build
```

## Step 2: Install Ruby
Once rbenv is ready you can execute the following command to install ruby with the version you specify

```
rbenv install 1.9.3-p545
```

*Sure, you can also install another version of ruby*

## Step 3: Set the global ruby version
If you are running `ruby -v` now you will see that there is no ruby installed (not really true). So this should tell you, that there is a version that is using the ruby command.

```
rbenv global 1.9[tab]
```
If you type 1.9 and then press TAB the Terminal should autocomplete the command and tell you the installed versions of ruby.

**Finished!** The version of ruby is now 1.9.3-p545

## Step 4: Install Rails and Passenger
Now everything is just easy when you have rbenv and RubyGems installed (RubyGems is installed automatically with ruby via rbenv). Just install rails and passenger via RubyGems like this:

```
gem install rails
gem install passenger
```

## Step 5: Install nginx
To run the Rails on Nginx on server you _must_ install Passenger and run this two more lines in the terminal:

```
rbenv rehash
passenger-install-nginx-module
```

And now Passenger takes over.

Passenger first checks that all of the dependencies it needs to work are installed. If you are missing any, Passenger will let you know how to install them with the apt-get installer on Debian. 

**Please install nginx in the default directory suggested by passenger**

After you download any missing dependencies, restart the installation. Type: passenger-install-nginx-module once more into the command line. 

Passenger offers users the choice between an automated setup or a customized one. Press 1 and enter to choose the recommended, easy, installation.

## Step 6: Create a nginx init-script
Put those lines into the terminal to clone the init script from linode to your server.
```
wget -O init-deb.sh http://library.linode.com/assets/660-init-deb.sh
sudo mv init-deb.sh /etc/init.d/nginx
sudo chmod +x /etc/init.d/nginx
sudo /usr/sbin/update-rc.d -f nginx defaults
```

## Step 7: Install and configurate Capistrano
*Note to myself: Insert some content for easy Capistrano installation and configuration*

## Step 8: Deploy your application to the server
*Note to myself: Insert some content for easy deployment of your application to the server*

## Step 9: Connect nginx to your rails project
To connect nginx to your rails project it is essential to put a server block into your nginx configuration:

```
vim /opt/nginx/conf/nginx.conf
```

and insert the following snippet:

```
server { 
  listen 80; 
  server_name example.com; 
  passenger_enabled on; 
  root /home/deploy/{APP_NAME}/public; 
}
```

### Step 10: Have fun with the server
Do whatever you want now.

**Note:** Sure, you could also upload your rails application via a [traditional ftp service](http://stackoverflow.com/questions/12608933/is-it-possible-to-ftp-a-rails-app-to-a-linux-server), but imho you will be very dumb if you do!