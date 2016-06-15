PagoSim<br>Geração de leads para crédito e cobrança
====
Ajudamos pessoas endividadas a localizar suas dívidas e estimamos um valor justo para seus débitos, factível para os credores, em cima da qual podem se organizar financeiramente e entregamos leads qualificados para empresas interessadas na negociação de dívidas, de pessoas que há muito tempo vêm sendo procuradas, sem sucesso, por seus credores.

Informações gerais
===

* A comunicação feita sobre um protocolo de comunicação criptografado (HTTPS).
* Todos os dados trafegádos estarão no formato [JSON](http://www.json.org/).


Leads para crédito
====

Acesse o seguinte serviço para obter os dados de um lead para crédito

<pre>
curl -X GET -d https://api.pagosim.com.br/v2/prospects/codigo-utm_uuid_que-voce-recebeu-na-url
</pre>

*Códigos HTTP de retorno*

| HTTP code |                   Descrição                                   |
|-----------|---------------------------------------------------------------|
| 403       |                   Acesso negado.                              |
| 404       |                   Lead não encontrado.                        |
| 200       |                   Lead encontrado.                            |

<pre>
<b>Conteúdo da resposta que devolvemos na requisição (quando o código HTTP for 200)</b>
{
    {
        "personalInfo":
            {
                "document":"14334758045", /* CPF do lead */
                "email":"darth.vader@darksideforce.com",
                "name":"Darth Vader",
                "phone":"+55116669996660",
                "birthday":"27/02/1980", /* pode ser nulo */
                "mothersName":"Shmi Skywalker" /* pode ser nulo */,
                "gender":"male|female" /* pode ser nulo */
            },
        "locationInfo":
            {
                "state":"SP", /* Estado (UF) */
                "city":"São Paulo" /* Cidade */
            },
        "loanInfo":
            {
                "product":"Cartão de crédito" /*Produto escolhido pelo usuário*/, 
                "personType":"payer|debtor" /*payer = pessoa sem negativação; debtor=pessoa com negativação */,
                "bank":"Itaú" /*Nome do banco que a pessoa possue conta corrente*/,
                "incomeValue":"Até R$ 2.500,00" /*Faixa de renda informada*/,
                "loanAmount":"R$ 5.000,00" /*Valor de empréstimo pretendido pela pessoa*/
            }
    }
}
</pre>

UUID para você testar: 254faa4b-6f9f-4230-b8c0-5aef2ba2b328

*Esse código estará presente na URL toda vez que o lead for direcionado para o seu site. Exemplo:*
<pre>
https://www.seusite.com.br?utm_uuid=254faa4b-6f9f-4230-b8c0-5aef2ba2b328
</pre>

Leads para cobrança
====

Acesse o seguinte serviço para obter o CPF de um lead para cobrança

<pre>
curl -X GET -d https://api.pagosim.com.br/v1/debtors/codigo-lead-pagosim
</pre>

*Abaixo estão listados os códigos HTTP de retorno que iremos tratar.*

| HTTP code |                   Descrição                                   |
|-----------|---------------------------------------------------------------|
| 403       |                   Acesso negado.                              |
| 404       |                   Lead não encontrado.                        |
| 200       |                   Lead encontrado.                            |

<pre>
<b>Conteúdo da resposta que devolvemos na requisição (quando o código HTTP de resposta for 200)</b>
{
    "utm_uiid": "número de identificação interno - o mesmo código que iremos mandar para você na URL",
    "document":"CPF da pessoa"
}
</pre>

Acesse o seguinte serviço para obter as informações cadastrais de um lead para cobrança

<pre>
curl -X GET --user seu-usuario-pagosim:sua-senha-pagosim -d https://api.pagosim.com.br/v1/debtors/document/cpf-do-lead
</pre>

*Abaixo estão listados os códigos HTTP de retorno que iremos tratar.*

| HTTP code |                   Descrição                                   |
|-----------|---------------------------------------------------------------|
| 403       |                   Acesso negado.                              |
| 404       |                   Lead não encontrado.                        |
| 200       |                   Lead encontrado.                            |

<pre>
<b>Conteúdo da resposta que devolvemos na requisição (quando o código HTTP de resposta for 200)</b>
{
    "personalInfo":
        {
            "document":"14334758045", /* CPF do lead */
            "email":"darth.vader@darksideforce.com",
            "name":"Darth Vader",
            "phone":"+55116669996660",
            "birthday":27/02/1980, /* pode ser nulo */
            "mothersName":Shmi Skywalker /* pode ser nulo */,
            "gender":male|female /* pode ser nulo */
        }
    "locationInfo":
        {
            "state":"SP", /* Estado (UF) */
            "city":"São Paulo" /* Cidade */
        },
    "dealInfo":
        {
            "payValue":"Quanto o usuário tem disponível para fazer o acordo"
            "payWhen": "Quando o usuário está disposto a fazer o pagamento"
        }
}
</pre>

Qualquer dúvida entre em [contato](mailto:devops@pagosim.com.br) com a gente ;)
