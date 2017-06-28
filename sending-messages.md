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

    $keyboard = (new Keyboard)
        ->addButton(
            (new Keyboard\ReplyButton)->setLabel('Yes, please.')
        )
        ->addButton(
            (new Keyboard\ReplyButton)->setLabel('No.')
        );

    $this->sendMessage('Should I send you a weather forecast every day?', $keyboard);

You can find out about supported templates in the [templates](/templates) section.

## Attachments
Sending attachment is an ease:

    $attachment = (new Attachment)
        ->setPath('http://lorempixel.com/400/200/')
        ->setType(Attachment::TYPE_IMAGE);
        
    $this->sendAttachment($attachment);

Naturally, delay is also supported in attachment sending:

    $attachment = (new Attachment)
        ->setPath('http://lorempixel.com/400/200/')
        ->setType(Attachment::TYPE_IMAGE);
        
    $this->sendAttachment($attachment, 3);

