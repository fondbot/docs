# Facebook

In order to create Facebook channel you need to create bot and obtain tokens.

You can find all related information in the [official guide](https://developers.facebook.com/docs/messenger-platform/guides/quick-start). 

## Installation

In your project root run the following command:

    php bin/toolbelt driver:install facebook

### Configuration    

Define Facebook channel in `src/Providers/ChannelServiceProvider.php`:

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

You can find route URL for your channels by running:

    php bin/toolbelt channel:list

## Templates

### Call Button

    $keyboard = (new Keyboard)
        ->addButton(
            (new CallButton)->setLabel('Call Representative')->setPhone('+15105551234')
        );
    
    $this->sendMessage('Need further assistance? Talk to a representative.', $keyboard);

### Share Button

    $keyboard = (new Keyboard)
        ->addButton(new ShareButton);
    
    $this->sendMessage('You can share this message.', $keyboard);

### Log In Button

    $keyboard = (new Keyboard)
        ->addButton(
            (new LogInButton)->setUrl('https://www.example.com/authorize')
        );
    
    $this->sendMessage('Press button below in order to link your account.', $keyboard);

### Log Out Button

    $keyboard = (new Keyboard)
        ->addButton(new LogOutButton);
    
    $this->sendMessage('Do you want to log out?', $keyboard);

### List Template

    $this->sendMessage(
        'T-shirts',
        (new ListTemplate)
            ->addElement(
                (new ListTemplate\Element)
                    ->setTitle('Classic T-Shirt Collection')
                    ->setSubtitle('See all our colors')
                    ->setImageUrl('https://peterssendreceiveapp.ngrok.io/img/collection.png')
                    ->setDefaultAction(
                        (new UrlButton)
                            ->setUrl('https://peterssendreceiveapp.ngrok.io/shop_collection')
                    )
            )
            ->addElement(
                (new ListTemplate\Element)
                    ->setTitle('Classic White T-Shirt')
                    ->setImageUrl('https://peterssendreceiveapp.ngrok.io/img/white-t-shirt.png')
                    ->setSubtitle('100% Cotton, 200% Comfortable')
            )
    );

### Receipt Template

    $this->sendMessage(
        'Order confirmation',
        (new ReceiptTemplate)
            ->setOrderNumber('12345678902')
            ->setCurrency('USD')
            ->setPaymentMethod('VISA 2345')
            ->setTimestamp((string) time())
            ->setRecipientName('Stephane Crozatier')
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
