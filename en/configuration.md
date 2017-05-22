# Configuration
All configuration is done by service providers which you can find in `src/Providers` folder. 
In order to keep sensitive and dynamic values you should use `.env` file which stand for environment configuration.

## Application
There is no need to change default application configuration, but you free to change it anyway in `src/Providers/AppServiceProvider.php`.

## Cache
By default FondBot will utilize filesystem for cache. You can change adapter in `src/Providers/CacheServiceProvider.php`.

## Channels
These are connections to different platforms (Telegram, Facebook Messenger, etc.). Define them in `src/Providers/ChannelServiceProvider.php`.

## Filesystem
FondBot uses League's [Flysystem](https://flysystem.thephpleague.com) package to work with filesystem. 

You can define Dropbox, Amazon S3, FTP and many other adapters in `src/Providers/FilesystemServiceProvider.php`.

## Intents
Intents are one of the core modules of FondBot. Define intents for your bot in `src/Providers/IntentServiceProvider.php`.

## Logging
FondBot uses [Monolog](https://seldaek.github.io/monolog/) to work with logs.
Define your own adapters in `src/Providers/LogServiceProvider.php`.

## Queues
As your bot become popular there will be many incoming requests. 
In order to send messages asynchronously you can use queues. 
By default `SyncAdapter` will be used and messages will be sent synchronously.

### Beanstalkd
FondBot comes with [Beanstalkd](http://kr.github.io/beanstalkd/) adapter.
If you want to use Beanstalkd, firstly install `pda/pheanstalk` package:

    composer require pda/pheanstalk:^3.1
    
Then, run queue worker:

    php bin/toolbelt queue:worker
    
### Supervisor
Use the following supervisor configuration in order to run worker in background:

    [program:fondbot-worker]
    process_name=%(program_name)s_%(process_num)02d
    command=php /var/www/fondbot/bin/toolbelt queue:worker
    autostart=true
    autorestart=true
    user=www-data
    numprocs=4
    redirect_stderr=true
    stdout_logfile=/var/www/fondbot/resources/logs/worker.log
