PagoSim<br>Auto atendimento para o setor de cobrança
====

Somos um [canal de auto atendimento](http://www.slideshare.net/pagosim/apresentao-comercial-pagosim) para o setor de cobrança.


Informações gerais
===

* A comunicação feita entre os nossos servidores precisa ser feita sobre um protocolo de comunicação criptografado (HTTPS).
* Todos os dados trafegádos deverão estar, obrigatoriamente, no formato [JSON](http://www.json.org/).


Autenticando nossa plataforma no seu sistema
====

Vamos chamar o seu serviço de autorização para obter o nome e o valor do pârametro que devemos utilizar para chamar os outros serviços:

<pre>
curl -X GET -d [https://seuwebservice.com.br/autenticacao]<b>[Nossas credenciais]</b>
</pre>

*Abaixo estão listados os códigos HTTP de retorno que iremos tratar.*

| HTTP code |                   Descrição                                   |
|-----------|---------------------------------------------------------------|
| 403       |                   Acesso negado.                              |
| 200       |                   Acesso concedido.                           |

<pre>
<b>Exemplo de resposta que esperamos receber (quando o código HTTP for igual a 200)</b>
{
    "tokenName": "NR_TOKEN",
    "tokenValue": "kCMN7jvUvUx5eb"
}
</pre>

Dívidas e Acordos
====

__Vamos fazer a seguinte chamada para obter as dívidas associadas ao CPF passado como parâmetro__<br/>
<pre>
curl -X GET [https://seuwebservice.com.br/dividas]<b>[CPF=666777888999&NR_TOKEN=kCMN7jvUvUx5eb]</b>

/*Os seguintes parâmetros serão passados na chamada*/
| Nome do parâmetros |     Tipo      |  Descrição                                     
|--------------------|-----------------------------------------------------------------------------------
|       CPF          |    string     |  CPF informado pelo usuário do PagoSim.        
|--------------------|-----------------------------------------------------------------------------------
|                    |               |  Nome do parâmetro que capturamos na autenticação e vamos enviar 
|    NR_TOKEN        |    string     |  para que o seu servidor reconheça, através do valor do parâmetro, 
|                    |               |  a nossa conexão. 
---------------------------------------------------------------------------------------------------------
</pre>

*Abaixo estão listados os códigos HTTP de retorno que iremos tratar.*

| HTTP code |                 Descrição                                     |
|-----------|---------------------------------------------------------------|
| 403       |                 Cliente não pode negociar através do PagoSim. |
| 404       |                 Cliente não encontrado.                       |
| 200       |                 Dividas encontradas.                          |

<pre>
<b>Exemplo de resposta que esperamos receber (quando o código HTTP for igual a 200)</b>
{
    "document": "6666667778889",
    "name": "Darth Vader",
    "birthDate": "25051977",
    "maritalStatus": "divorciado",
    "sex": "masculino",
    "debts": [
        {
            "id": "1234566767",
            "currentValue": 1000.82,
            "timeDelayInDays": 180,
            "proposals": [
                {
                    "numberOfInstallments": 1,
                    "value": 200.16
                },
                {
                    "numberOfInstallments": 3,
                    "value": 133.44
                }
            ]
        }
    ]
}
</pre>

__Vamos fazer a seguinte chamada para informar que um acordo foi fechado com o cliente__<br/>
<pre>
curl -X POST -d "<b>NR_TOKEN=kCMN7jvUvUx5eb&debitId=1234566767&numberOfInstallments=3</b>" [https://seuwebservice.com.br/acordo]

/*Os seguintes parâmetros serão passados na chamada*/
| Nome do parâmetros   |    Tipo    |    Descrição                                     
|----------------------|------------------------------------------------------------------------------------
|      debitId         |   string   |    Identificador da dívida fornecida por vocês.        
|----------------------|------------------------------------------------------------------------------------
| numberOfInstallments |   integer  |    Quantidade de parcelas escolhidas para fechar o acordo.        
|----------------------|------------------------------------------------------------------------------------
|                      |            |     Todos os dados para contato informado pelo usuário serão enviados
|                      |            |     parâmetro. Abaixo um exemplo de preenchimento deste parâmetro.
|                      |            |      
|                      |            |     user: { email:'darthvader@starwars.com',
|                      |            |             address: { zipCode:66666090,
|       user           |    json    |                        street:'av paulista', 
|                      |    object  |                        number:1877, 
|                      |            |                        additionalInfo:'ap 67',
|                      |            |                        city:'Sao Paulo',
|                      |            |                        state:'SP' }
|                      |            |                        }
|----------------------|------------------------------------------------------------------------------------
|                      |            |     Nome do parâmetro que capturamos na autenticação e vamos enviar 
|    NR_TOKEN          |    string  |     para que o seu servidor reconheça, através do valor do parâmetro, 
|                      |            |     a nossa conexão.
|----------------------|------------------------------------------------------------------------------------


</pre>

*Abaixo estão listados os códigos HTTP de retorno que iremos tratar.*

| HTTP code |                 Descrição                                     |
|-----------|---------------------------------------------------------------|
| 403       |                 Número de parcelas do acordo não é permitida. |
| 404       |                 Cliente não encontrado.                       |
| 200       |                 Acordo fechado com sucesso.                   |

<pre>
<b>Exemplo de resposta que esperamos receber (quando o código HTTP for igual a 200)</b>
{
    "dealId": "4564545645",
    "dueDate": "30102016"
}
</pre>

Qualquer dúvida entre em [contato](mailto:devops@pagosim.com.br) com a gente ;) 

