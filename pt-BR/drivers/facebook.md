# Facebook

In order to create Facebook channel you need to create bot and obtain tokens.
Para criar o canal do Facebook você precisa criar um bot e obter as chaves de token.

Você pode encontrar mais informações no [guia oficial](https://developers.facebook.com/docs/messenger-platform/guides/quick-start).

## Instalação

Na raiz do projeto execute o comando:

    php bin/toolbelt driver:install facebook

### Configuração    

Defina o canal do Facebook em `src/Providers/ChannelServiceProvider.php`:

    public function channels(): array
    {
        return [
            'facebook' => [
                'driver' => 'facebook',
                'page_token' => env('FACEBOOK_PAGE_TOKEN'),
                'verify_token' => env('FACEBOOK_VERIFY_TOKEN'),
                'app_secret' => env('FACEBOOK_APP_SECRET'),
            ],
        ];
    }

### Webhook URL

Você pode encontrar as rota para as URL dos seus canais pelo comando:

    php bin/toolbelt channel:list

## Templates

### Call Button

    $keyboard = (new Keyboard)
        ->addButton(
            (new CallButton)->setLabel('Ligar para Atendente')->setPhone('+5521999999999')
        );

    $this->sendMessage('Precisa de mais ajuda? Fale com um atendente.', $keyboard);

### Botão de compartilhamento

    $keyboard = (new Keyboard)
        ->addButton(new ShareButton);

    $this->sendMessage('Você pode compartilhar esta mensagem.', $keyboard);

### Botão de Login

    $keyboard = (new Keyboard)
        ->addButton(
            (new LogInButton)->setUrl('https://www.example.com/authorize')
        );

    $this->sendMessage('Aperte o botão abaixo para fazer login.', $keyboard);

### Botão de Logout

    $keyboard = (new Keyboard)
        ->addButton(new LogOutButton);

    $this->sendMessage('Você quer sair?', $keyboard);

### Lista

    $this->sendMessage(
        'Camisas',
        (new ListTemplate)
            ->addElement(
                (new ListTemplate\Element)
                    ->setTitle('Coleção clássica de camisas')
                    ->setSubtitle('Veja todas as cores')
                    ->setImageUrl('https://peterssendreceiveapp.ngrok.io/img/collection.png')
                    ->setDefaultAction(
                        (new UrlButton)
                            ->setUrl('https://peterssendreceiveapp.ngrok.io/shop_collection')
                    )
            )
            ->addElement(
                (new ListTemplate\Element)
                    ->setTitle('Camisa Clássica Branca')
                    ->setImageUrl('https://peterssendreceiveapp.ngrok.io/img/white-t-shirt.png')
                    ->setSubtitle('100% Cotton, 200% Confortável')
            )
    );

### Cobrança

    $this->sendMessage(
        'Order confirmation',
        (new ReceiptTemplate)
            ->setOrderNumber('12345678902')
            ->setCurrency('BRL')
            ->setPaymentMethod('VISA 2345')
            ->setTimestamp((string) time())
            ->setRecipientName('Jhon Doe')
            ->setOrderUrl('http://petersapparel.parseapp.com/order?order_id=123456')
            ->setAddress(
                (new ReceiptTemplate\Address)
                    ->setCity('Menlo Park')
                    ->setCountry('US')
                    ->setPostalCode('94025')
                    ->setState('CA')
                    ->setStreet1('1 Hacker Way')
                    ->setStreet2('')
            )
            ->setSummary(
                (new ReceiptTemplate\Summary)
                    ->setShippingCost(4.95)
                    ->setSubtotal(75)
                    ->setTotalTax(6.19)
                    ->setTotalCost(56.14)
            )
            ->addElement(
                (new ReceiptTemplate\Element)
                    ->setTitle('Classic White T-Shirt')
                    ->setSubtitle('100% Soft and Luxurious Cotton')
                    ->setCurrency('USD')
                    ->setPrice(50)
                    ->setQuantity(2)
                    ->setImageUrl('http://petersapparel.parseapp.com/img/whiteshirt.png')
            )
            ->addElement(
                (new ReceiptTemplate\Element)
                    ->setTitle('Classic Gray T-Shirt')
                    ->setSubtitle('100% Soft and Luxurious Cotton')
                    ->setCurrency('USD')
                    ->setPrice(25)
                    ->setQuantity(1)
                    ->setImageUrl('http://petersapparel.parseapp.com/img/grayshirt.png')
            )
            ->addAdjustment(
                (new ReceiptTemplate\Adjustment)
                    ->setAmount(20)
                    ->setName('New Customer Discount')
            )
            ->addAdjustment(
                (new ReceiptTemplate\Adjustment)
                    ->setAmount(10)
                    ->setName('$10 Off Coupon')
            )
    );
