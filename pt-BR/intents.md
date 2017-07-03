# Intent

## Introdução
Na execução você poderá enviar mensagens, anexos e templates.

Para criar um dialogo e processar as respostas do usuário você precisa utilizar as [interactions](/interactions)

## Creating Intents
Crie uma nova Intent pela toolbelt com o comando:

    php bin/toolbelt make:intent Clima

O comando irá gerar o arquivo `src/Intents/ClimaIntent.php` que irá conter a seguinte classe:

    <?php

    declare(strict_types=1);

    namespace Bot\Intents;

    use FondBot\Conversation\Activators\Activator;
    use FondBot\Conversation\Intent;
    use FondBot\Drivers\ReceivedMessage;
    use GuzzleHttp\Client;

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
                $this->exact(`/clima`),
                $this->exact(`Como está o tempo hoje?`),
            ];
        }

        public function run(ReceivedMessage $message): void
        {
            // Busca os dados do clima
            $guzzle = new Client;
            $response = $guzzle->get(`http://samples.openweathermap.org/data/2.5/weather?q=Rio de janeiro,br&appid=b1b15e88fa797225412429c1c50c122a1`);
            $response = json_decode($response->getBody()->getContents());

            // Envia uma resposta ao usuário
            $this->sendMessage($response->weather->description);
        }
    }


## Ativadores
No exemplo acima, se o usuário enviar `/clima` ou `Como está o clima hoje?` então a `ClimaIntent` será ativada.

### Ativadores Disponiveis

#### Ativador Exact
O Ativador exact funciona quando a mensagem de texto e o valor do ativador são iguais. Você pode pssar um segundo argumento para informar e as strings deverão ser case sensitive.

| Class                                 | Helper method  |
|---------------------------------------|----------------|
| FondBot\Conversation\Activators\Exact | $this->exact() |

#### Ativador Contains
O Ativador contains funciona quando a mensagem de texto contem um ou mais valores.

| Class                                    | Helper method     |
|------------------------------------------|-------------------|
| FondBot\Conversation\Activators\Contains | $this->contains() |

#### Ativador Pattern
O Ativador Pattern verifica se a mensagem atende a uma expressão regular.

| Class                                   | Helper method    |
|-----------------------------------------|------------------|
| FondBot\Conversation\Activators\Pattern | $this->pattern() |

#### Ativador In Array
O Ativador In Array verifica se a mensagem de texto está contida em uma Array.

| Class                                   | Helper method    |
|-----------------------------------------|------------------|
| FondBot\Conversation\Activators\InArray | $this->inArray() |

#### Ativador With Attachment
O Ativador With Attachment verifica se a mensagem contém um anexo (image, arquivo, etc.). Você pode especificar o tipo de anexo que deve ser enviado.

| Class                                          | Helper method           |
|------------------------------------------------|-------------------------|
| FondBot\Conversation\Activators\WithAttachment | $this->withAttachment() |

## Entendendo uma Intent
Quando um dos ativadores da intent é chamado, o método `run` será executado pelo framework.
Aqui você pode fazer algumas requisições, por exemplo, retornar dados de uma API externa e retornar o resultado para o usuário.
Vá para a seção [sending messages](/sending-messages) para entender um pouco melhor sobre os templates de mensagem.

Ah, se você quiser criar um dialogo com o usuário processando a respota dele, você precisa executar uma [interaction](/interactions) na Intent:

    public function run(ReceivedMessage $message): void
    {
        $this->jump(Interactions\PerguntarCidadeInteraction::class);
    }
