# VK Communities

You can find all information about setting callbacks for your VK community bot in the [official documentation](https://vk.com/dev/bots_docs).

## Installation

In your project root run the following command:

    php bin/toolbelt driver:install vk-communities

### Configuration    

Define VK Communities channel in `src/Providers/ChannelServiceProvider.php`:

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

### Registering Webhook

You can find route URL for your channels by running:

    php bin/toolbelt channel:list