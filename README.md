PagoSim<br>Geração de leads para crédito e cobrança
====
Somos uma consultoria financeira gratuita para as pessoas e que tem como modelo de negócio a geração de leads qualificados para os setores de crédito e cobrança.

Informações gerais
===

* A comunicação feita sobre um protocolo de comunicação criptografado (HTTPS).
* Todos os dados trafegádos estarão no formato [JSON](http://www.json.org/).


Verificando leads para crédito
====

Acesse o seguinte serviço para obter os dados de um lead para crédito

<pre>
curl -X GET -d [https://api.pagosim.com.br/v2/prospects/codigo-utm_uuid_que-voce-recebeu-na-url]
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
                "document":"22366661878",
                "email":"darth.vader@darksideforce.com",
                "name":"Darth Vader",
                "phone":"+55116669996660",
                "birthday":null, /* formato da data QUANDO estiver presente: 27/02/1980" */
                "mothersName":null
            },
        "locationInfo":
            {
                "state":"SP" /* UF brasileira*/
            },
        "loanInfo":
            {
                "ProductName":"Empréstimo consignado", /* Produto escolhido pelo usuário */
                "isDebtor":true, /* Indica se a pessoa tem algum tipo de restrição financeira */
                "BankAccount":"Itaú", /* Nome do banco que a pessoa possue conta corrente */
                "IncomeClass":"Até R$ 2.500,00" /* Classe social da pessoa */
            }
    }
}
</pre>

<pre>
Exemplo de UTM_UUID para testes: 254faa4b-6f9f-4230-b8c0-5aef2ba2b328
[https://api.pagosim.com.br/v2/prospects/254faa4b-6f9f-4230-b8c0-5aef2ba2b328]
</pre>

Verificando leads para cobrança
====

Acesse o seguinte serviço para obter o CPF de um lead para cobrança

<pre>
curl -X GET -d [https://api.pagosim.com.br/v1/debtors/codigo-lead-pagosim]
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
curl -X GET -d [https://api.pagosim.com.br/v1/debtors/document/cpf-do-lead]
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
            "name": "Nome da pessoa",
            "document":"CPF da pessoa,
            "mail":"e-mail confirmado da pessoa",
            "phone":"telefone celular confirmado da pessoa -> +5511977668899",
            "mother":"Nome da mãe da pessoa",
            "birthday":"data de nascimento da pessoa -> 27/02/1980"
        }
}
</pre>

Qualquer dúvida entre em [contato](mailto:devops@pagosim.com.br) com a gente ;)
