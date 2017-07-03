# Telegram

Para criar o canal do Facebook você precisa criar um bot e obter as chaves de token.

Você pode encontrar mais informações no [guia oficial](https://core.telegram.org/bots#3-how-do-i-create-a-bot).

## Installation

Na raiz do projeto execute o comando:

    php bin/toolbelt driver:install telegram

### Configuração    

Define Telegram channel in `src/Providers/ChannelServiceProvider.php`:

    public function channels(): array
    {
        return [
            'telegram' => [
                'driver' => 'telegram',
                'token' => env('TELEGRAM_TOKEN'),
            ],
        ];
    }

### Registrando o Webhook
O Telegram requer o protocolo HTTPS para as urls de webhook. Leia mais sobre os Webhooks do Telegram no [guia oficial](https://core.telegram.org/bots#3-how-do-i-create-a-bot).

Então, utilize o curl para dizer ao Telegram qual URL utilizar para se comunicar com o bot:

    curl -F “url=https://<YOURDOMAIN>/<WEBHOOKLOCATION>" https://api.telegram.org/bot<TOKEN-OBTAINED-FROM-TELEGRAM>/setWebhook    

Você pode encontrar as rota para as URL dos seus canais pelo comando:


    php bin/toolbelt channel:list

## Templates

### Pedir Telefone

    $keyboard = (new Keyboard)
        ->addButton(
            (new RequestContactButton)->setLabel('Enviar meu número de telefone.')
        );

    $this->sendMessage('Qual o seu número de telefone? Nosso atendimento irá te ligar.', $keyboard);

### Pedir Localização

    $keyboard = (new Keyboard)
        ->addButton(
            (new RequestLocationButton)->setLabel('Enviar minha localização.')
    );
