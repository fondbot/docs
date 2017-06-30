# Interactions

## Introdução
Interaction is used when bot needs to process user reply aka dialog.
Uma Interaction será utilizada quando o bot precisa processar a resposta do usuário, ou seja, um diálogo.

O bot pode chamar  interaction através de uma [intent](/intents) utilizando o método 'jump'.

## Criando uma Interaction

Para criar uma nova interaction, execute o comando da toolbelt:

    php bin/toolbelt make:interaction PergutnarCidadeCity

O comando irá gerar o arquivo `src/Interactions/PerguntarCidadeInteraction.php` que contém a seguinte classe:

    <?php

    declare(strict_types=1);

    namespace Bot\Interactions;

    use FondBot\Conversation\Interaction;
    use FondBot\Drivers\ReceivedMessage;
    use GuzzleHttp\Client;

    class PerguntarCidadeInteraction extends Interaction
    {
        /**
         * Run interaction.
         *
         * @param ReceivedMessage $message
         */
        public function run(ReceivedMessage $message): void
        {
            $this->sendMessage('Onde você está?');
        }

        /**
         * Process received message.
         *
         * @param ReceivedMessage $reply
         */
        public function process(ReceivedMessage $reply): void
        {
            // O Bot só pode encontrar informações para algumas cidades
            $city = $reply->getText();
            $cities = ['Rio de Janeiro', 'São Paulo', 'Belo Horizonte'];
            if (!in_array($city, $cities, true)) {
                $this->sendMessage(
                    'Infelizmente eu só posso encontrar informações do clima para ' . implode($cities, ', ') . '.'
                );

                $this->restart();

                return;
            }

            // Busca os dados do clima
            $guzzle = new Client;
            $response = $guzzle->get('http://samples.openweathermap.org/data/2.5/weather?q=Rio de janeiro,br&appid=b1b15e88fa797225412429c1c50c122a1');
            $response = json_decode($response->getBody()->getContents());

            // Envia uma resposta ao usuário
            $this->sendMessage($response->weather->description);
        }
    }

## Entendendo uma Interaction  
Quando o bot chama uma Interaction, o farmework irá executar o metodo 'run'.  
Nesse metodo você precisa enviar alguma pergunta/opção par ao usuário para receber uma resposta..

Depois o bot irá esperar o usuário responder e quando a mensagem for recebida o método 'process' será executado.
Aqui você pode enviar uma mensagem para o usuário novamente. Você pode reiniciar a interaction, caso algo de errado ou o usuário não responder corretamente, ou pular para outra Interaction.

Se você não reiniciar a Interaction ou não pular para outra Interaction, a sessão atual será encerrada e o bot estará pronto para ativar as Intents novamente.
