# Intent

## Introduction
Intent is a command which is been executed upon activation.
Upon running you can send messages, attachments and templates.

In order to create dialog and process user replies you need to create [interaction](/interactions).

## Creating Intents

Create new intent by running toolbelt command:

    php bin/toolbelt make:intent Weather

This command will generate `src/WeatherIntent.php` file which will contain the following class:

    <?php

    declare(strict_types=1);

    namespace App;

    use FondBot\Conversation\Activators\Activator;
    use FondBot\Conversation\Intent;

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
            ];
        }

        public function run(): void
        {
            // Send reply to user, jump to interaction or do something else...
        }
    }


## Activators

Activator is trigger for an intent. From the above example, whenever user types `/weather` intent will run.

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