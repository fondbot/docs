# Intent

## Introduction
Intent is a command which is been executed upon activation.
Upon running you can send messages, attachments and templates.

In order to create dialog and process user replies you need to use [interactions](/interactions).

## Creating Intents
Create new intent by running toolbelt command:

    php bin/toolbelt make:intent Weather

This command will generate `src/WeatherIntent.php` file which will contain the following class:

    <?php
    
    declare(strict_types=1);
    
    namespace App;
    
    use FondBot\Conversation\Activators\Activator;
    use FondBot\Conversation\Intent;
    use FondBot\Drivers\ReceivedMessage;
    use GuzzleHttp\Client;
    
    class WeatherIntent extends Intent
    {
        /**
         * Intent activators.
         *
         * @return Activator[]
         */
        public function activators(): array
        {
            return [
                $this->exact('/weather'),
                $this->exact('Tell me the weather for today'),
            ];
        }
    
        public function run(ReceivedMessage $message): void
        {
            // Fetch weather data
            $guzzle = new Client;
            $response = $guzzle->get('http://samples.openweathermap.org/data/2.5/weather?q=London,uk&appid=b1b15e88fa797225412429c1c50c122a1');
            $response = json_decode($response->getBody()->getContents());
            
            // Send result to user
            $this->sendMessage($response->weather->description);
        }
    }


## Activators
From the above example, if user sends `/weather` or `Tell me the weather for today` then `WeatherIntent` will be activated. 

### Available Activators

#### Exact Activator
The Exact activator works when message text and activator's value are equivalent. You can also pass a second argument to set if strings must be case sensitive.

| Class                                 | Helper method  |
|---------------------------------------|----------------|
| FondBot\Conversation\Activators\Exact | $this->exact() |

#### Contains Activator
The Contains activator works when message text contains one or more values.

| Class                                    | Helper method     |
|------------------------------------------|-------------------|
| FondBot\Conversation\Activators\Contains | $this->contains() |

#### Pattern Activator
The Pattern activator checks if message text is matched by a regular expression.

| Class                                   | Helper method    |
|-----------------------------------------|------------------|
| FondBot\Conversation\Activators\Pattern | $this->pattern() |

#### In Array Activator
The In Array activator checks if message text matches one of the values from the array.

| Class                                   | Helper method    |
|-----------------------------------------|------------------|
| FondBot\Conversation\Activators\InArray | $this->inArray() |

#### With Attachment Activator
The With Attachment activator works if message contains attachment. You can also set which attachment type should exactly be.

| Class                                          | Helper method           |
|------------------------------------------------|-------------------------|
| FondBot\Conversation\Activators\WithAttachment | $this->withAttachment() |

## Handling Intent
When one of the intent activator matches, `run` method will be executed by framework.
Here you can do some tasks like fetching data from external API and then sending result to the user.
Go to the [sending messages](/sending-messages) section to learn more about message templates.

Also, if you want to create dialog with user with processing his reply you need to run [interaction](/interactions) within the intent:

    public function run(ReceivedMessage $message): void
    {
        $this->jump(Interactions\AskCityInteraction::class);
    }

