# Enviando Mensagens
Você só pode enviar mensagens de uma Intent ou Interaction.

## Text With Template
Para enviar uma mensagem de text com ou sem um template, em uma Intent ou Interaction, utilize o método `sendMessage`:

### Mensagem Básica
    <?php

    declare(strict_types=1);

    namespace App;

    use FondBot\Conversation\Activators\Activator;
    use FondBot\Conversation\Intent;
    use FondBot\Drivers\ReceivedMessage;

    class ClimaIntent extends Intent
    {
        /**
        * Intent activators.
        *
        * @return Activator[]
        */
        public function activators(): array
        {
            return [
                $this->exact('/clima'),
                $this->exact('Como está o clima hoje?'),
            ];
        }

        public function run(ReceivedMessage $message): void
        {
            $this->sendMessage('O clima está bom hoje.');
        }
    }

### Mensagem Atrasada
Se você quiser enviar uma mensagem com algum atraso, passe o numero de segundos como terceiro argumento:

    $this->sendMessage('Se você precisa de mais alguma ajuda digite /ajuda.', null, 3);

From the above example a message with `If you need an additional information type /help.` text will be sent in 3 seconds.
No exemplo acima a mnsagem com 'Se você precisa de mais alguma ajuda digite /ajuda.' será enviada em 3 segundos.

### Enviando Templates
O FondBot pode enviar templates. Passe o objeto do template como segundo argumento no método 'sendMessage':

    $keyboard = (new Keyboard)
        ->addButton(
            (new Keyboard\ReplyButton)->setLabel('Sim, por favor.')
        )
        ->addButton(
            (new Keyboard\ReplyButton)->setLabel('Não.')
        );

    $this->sendMessage('Posso te enviar a previsão do tempo todos os dias?', $keyboard);

Você pode encontrar os templates suportados em [templates](/templates).

## Anexos
Envie anexos facilmente:

    $attachment = (new Attachment)
        ->setPath('http://lorempixel.com/400/200/')
        ->setType(Attachment::TYPE_IMAGE);

    $this->sendAttachment($attachment);

Naturalmente você também pode enviar um anexo com atraso:

    $attachment = (new Attachment)
        ->setPath('http://lorempixel.com/400/200/')
        ->setType(Attachment::TYPE_IMAGE);

    $this->sendAttachment($attachment, 3);
