# Instalação

## Requerimentos
* PHP >= 7.1

## Instalando o FondBot
Utlize o comando `create-project` do composer para criar o projeto:

    composer create-project --prefer-dist fondbot/fondbot bot

Uma nova pasta chamada `bot` será criada. Agora vá para [configuration](/configuration) para começar a dar vida a seu bot.

## Permissões

O diretório `resources` deve ter permissão para escrita em seu servidor.
Você pode fazer isso alterando o dono da pasta para o usuário que roda o seu web server (Ex. www-data):

    chown -R www-data:www-data .

Ou altere todas as permissões na pasta `resources`:

    chmod -R 777 resources
