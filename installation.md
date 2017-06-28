# Installation

## Requirements
* PHP >= 7.1 

## Installing FondBot
Use Composer `create-project` command to bootstrap bot project:

    composer create-project --prefer-dist fondbot/fondbot bot

A new folder called `bot` will be created. Now go through [configuration](/configuration) section in order to tune created application.
    
## Directory Permissions

Directory `resources` should be writable by your web server. 
You can achieve this by changing the owner of the whole folder to the user which runs the web server (e.g. www-data):

    chown -R www-data:www-data .
    
Or setting full permissions on the `resources` folder:

    chmod -R 777 resources

