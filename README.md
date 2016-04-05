PagoSim<br>Geração de leads para crédito e cobrança
====
Somos uma consultoria financeira gratuita para as pessoas e que tem como modelo de negócio a geração de leads qualificados para os setores de crédito e cobrança.

Informações gerais
===

* A comunicação feita entre os nossos servidores precisa ser sobre um protocolo de comunicação criptografado (HTTPS).
* Nós precisamos dos IPs que irão acessar os nossos servidores.
* Todos os dados trafegádos deverão estar, obrigatoriamente, no formato [JSON](http://www.json.org/).


Verificando leads para crédito
====

Acesse o seguinte serviço para verificar se um CPF é um lead para crédito

<pre>
curl -X GET -d [https://api.pagosim.com.br/v1/payers/document/cpf-do-lead]
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
    "name": "Nome da pessoa",
    "document":"CPF da pessoa,
    "mail":"e-mail confirmado da pessoa",
    "phone":"telefone celular confirmado da pessoa - +5511977668899",
    "mother":"Nome da mãe da pessoa",
    "birthday":"data de nascimento da pessoa - dd/MM/yyyy"
}
</pre>

Verificando leads para cobrança
====

Acesse o seguinte serviço para verificar se um CPF é um lead para cobrança

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
    "utm_uiid": "número de identificação interno - o mesmo código que iremos mandar para você na URL",
    "name": "Nome da pessoa",
    "document":"CPF da pessoa,
    "mail":"e-mail confirmado da pessoa",
    "phone":"telefone celular confirmado da pessoa - +5511977668899",
    "mother":"Nome da mãe da pessoa",
    "birthday":"data de nascimento da pessoa - dd/MM/yyyy"
}
</pre>

Qualquer dúvida entre em [contato](mailto:devops@pagosim.com.br) com a gente ;)
