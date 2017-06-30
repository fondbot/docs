# Configuração
Todas as configurações são feitas pelos Service Providers que estão na pasta `src/Providers`.

Para manter os dados dinamicos, use o arquivo `.env`, que serve para a configuração do ambiente.

## Aplicação
Não é necessário alterar as configurações padrões da aplicação, mas você pode faze-la em `src/Providers/AppServiceProvider.php`.

## Cache
Por padrão o FondBot utilizará o filsystem para cache. Você pode mudar o adaptador em `src/Providers/CacheServiceProvider.php`.

## Channels
Existem conexões para diferentes plataformas (Telegram, Facebook Messenger, etc.) Você pode defini-los em `src/Providers/ChannelServiceProvider.php`.

## Filesystem
FondBot utiliza o package League`s [Flysystem](https://flysystem.thephpleague.com) para trabalhar com filesystem.


Você pode escolher entre Dropbox, Amazon S3, FTP e outros adaptadores em `src/Providers/FilesystemServiceProvider.php`.

## Intents
As Intents são um dos modulos principais do FondBot. Defina as Intents para o seu bot em `src/Providers/IntentServiceProvider.php`.

## Logging
FondBot utiliza o  [Monolog](https://seldaek.github.io/monolog/) para trabalhar com logs.
Defina seu própro adaptador em `src/Providers/LogServiceProvider.php`.

## Queues
Quando seu bot se tornar popular, haverão muitas requisições.
Para enviar mensagens de forma asíncrona, você pode usar as queues.
Por padrão o `SyncAdapter` será utilizado e as mensagens serão enviadas de forma síncrona.
Altere o adaptador em `src/Providers/QueueServiceProvider.php`.

### Beanstalkd
O FondBot vem com o adptador [Beanstalkd](http://kr.github.io/beanstalkd/).
Se você quiser utilizá-lo, primeiro installe o pacote `pda/pheanstalk`

    composer require pda/pheanstalk:^3.1

Então, execute o queue worker:

    php bin/toolbelt queue:worker

### Supervisor
Utilize a seguinte configuração de supervisor para rodar o worker em plano de fundo.

    [program:fondbot-worker]
    process_name=%(program_name)s_%(process_num)02d
    command=php /var/www/fondbot/bin/toolbelt queue:worker
    autostart=true
    autorestart=true
    user=www-data
    numprocs=4
    redirect_stderr=true
    stdout_logfile=/var/www/fondbot/resources/logs/worker.log
