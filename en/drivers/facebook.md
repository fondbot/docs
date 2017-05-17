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

If you use Laravel your url will look like:

    https://<YOURDOMAIN>/fondbot/<YOUR-FACEBOOK-CHANNEL-NAME>

## Templates