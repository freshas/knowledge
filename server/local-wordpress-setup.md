# Setup a wordpress server

### 1. Download the latest available version of wordpress:

- You can get it [here](https://wordpress.org/download/) by downloading and unzip the archive in an empty dir of your choice.
- Also you can open your Terminal, create, move into the new dir and type:
```bash
curl -fsSL https://wordpress.org/latest.tar.gz | tar -xz --strip-components 1
```

### 2. Install MAMP - PRO Version recommended.
Set an local URL for your Development in host settings.
Set the root to your previous created dir, where your wordpress should be placed.


### 3. Let's type some basic shell commands
First we need to navigate in our created dir and type :
```bash
mysql -u root [-p]
```
Currently Terminal asked you for an password you would like to use.

Now we're able to set up a new mysql database with the following command:
```mysql
create database DATABASENAME;
```
Don't forget to change DATABASENAME with the name of your choice.   

### 4. We are almost finished, just open your Browser and type the URL, which do you previous set in MAMP and follow the instructions of the wordpress interface.
