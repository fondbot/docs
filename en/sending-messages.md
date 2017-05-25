# Sending Messages
You are eligible for sending messages only from intents or interactions.

## Text With Template
In order to send message with text with or without template within intent or interaction use `sendMessage` method:

### Basic Message
    <?php

    declare(strict_types=1);

    namespace App;

    use FondBot\Conversation\Activators\Activator;
    use FondBot\Conversation\Intent;
    use FondBot\Drivers\ReceivedMessage;

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
            $this->sendMessage('The weather is fine today.');
        }
    }

### Delayed Message
If you want to send message with delay, pass the number of seconds to the third argument:

    $this->sendMessage('If you need an additional information type /help.', null, 3);

From the above example a message with `If you need an additional information type /help.` text will be sent in 3 seconds.

### Sending Templates
FondBot supports sending templates. Pass template object in the second argument to `sendMessage` method:

    $this->sendMessage(
        'Should I send you a weather forecast every day?',
        new Keyboard([
            new Keyboard\ReplyButton('Yes, please.'),
            new Keyboard\ReplyButton('No.'),
        ])
    );

You can find out about supported templates in the [templates](/templates) section.

## Attachments
Sending attachment is an ease:

    $this->sendAttachment(
        new Attachment(
            Attachment::TYPE_IMAGE,
            'https://fakeimg.pl/350x200/?text=FondBot'
        )
    );

Naturally, delay is also suppoted in attachment sending:


    $this->sendAttachment(
        new Attachment(
            Attachment::TYPE_IMAGE,
            'https://fakeimg.pl/350x200/?text=FondBot'
        ),
        3
    );

