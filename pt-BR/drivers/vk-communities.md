# VK Communities

You can find all information about setting callbacks for your VK community bot in the [official documentation](https://vk.com/dev/bots_docs).
Você pode encontrar as informações sobre callbacks para o seu bot na  [documentação oficial](https://vk.com/dev/bots_docs).

## Installation

Na raiz do projeto execute o comando:

    php bin/toolbelt driver:install vk-communities

### Configuração    

Defina o canal da VK Communities em `src/Providers/ChannelServiceProvider.php`:

    public function channels(): array
    {
        return [
            'vk-communities' => [
                'driver' => 'vk-communities',
                'access_token' => env('VK_COMMUNITIES_ACCESS_TOKEN'),
                'confirmation_token' => env('VK_COMMUNITIES_CONFIRMATION_TOKEN'),
            ],
        ];
    }

### Registrando o Webhook

Você pode encontrar as rota para as URL dos seus canais pelo comando:

    php bin/toolbelt channel:list
