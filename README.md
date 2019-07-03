# API
API public e de trade para usar na Bitcointoyou

 Documentação API

O acesso à nossa API e Trade API, é realizado via requisição HTTP POST com autorização no cabeçalho da solicitação (HTTP Header). O retorno sempre será em formato JSON. Sabendo que metodos da API Trade necessitam dos parametros de Autenticação.

URL: https://api_v1.bitcointoyou.com/METODO

Exemplo: URL: https://api_v1.bitcointoyou.com/ticker.aspx

API Trade

balance.aspx Retorna as informações da conta;

createorder.aspx Cria ordem de compra ou venda da moeda desejada;

deleteorders.aspx Realiza cancelamento da ordem desejada;

getorders.aspx Retorna as informações da ordem desejada;

getordersid.aspx Retorna as informações da ordem desejada passando como parâmetro o id;
API

orderbook.aspx Retorna as informações das ordem de compra e venda disponíveis de Bitcoin;

orderbook_litecoin.aspx Retorna as informações das ordem de compra e venda disponíveis de Litecoin;

ticker.aspx Retorna o ticker com o preço e volume do Bitcoin;

ticker_litecoin.aspx Retorna o ticker com o preço e volume do Litecoin;

trades.aspx Retorna as negociações realizadas;
Autenticação

Todas chamadas que necessitam de autenticação, deveram passar os seguintes parâmetros:

key Chave GUID fornecida no momento da geração da API;

nonce Número incremental a ser definido pelo desenvolvedor, o mesmo será salvo em sua primeira requisição na API;

signature BASE64(UPPER) HMAC-SHA256
BASE64(HMAC-SHA256(message, secret)).ToUpper(), onde:
Message = ACCESS_NONCE + ACCESS_KEY;
Secret = API Secret informado na tela de API (API.aspx);

Exemplos de como criar um HMAC-SHA256, acessse:

http://www.jokecamp.com/code/2012/10/21/examples-of-creating-base64-hashes-using-hmac-sha256-in-different-languages/
Acesso

Cada conta poderá relizar 1 requisição por segundo;
Retorno

Caso a solicitação seja bem sucedida, o retorno chegará no seguinte formato:


{
    "success": "1",
    "oReturn": <result>
}

Caso a solicitação não seja bem sucedida, o retorno chegará no seguinte formato:


{
    "success": "0",
    "error": <error> 
}

Métodos
balance.aspx

Autenticação

Sim

Parâmentros:

Não possui

Campos:

balanceAvailable Labellista saldo disponível para cada moeda(BRL, BTC e LTC)

timestamp timestamp retornado no momento absoluto da consulta;

Retorno:


{
  "success": "1",
  "oReturn": [
    {
      "BRL": 8657.531311027634275,
      "BTC": 35.460074025529646,
      "LTC": 9.840918628667236,
      "DOGE": 5419.490003406479187,
      "DRK": 0.121461143982142
    }
  ],
  "date": "2015-08-06 17:28:58.382",
  "timestamp": "1438882138"
}

createOrder.aspx

Autenticação

Sim

Parâmentros:

asset Identificação da moeda, na ordem a ser criada. Sendo BTC para Bitcoin e LTC para Litecoin;

action Ação da ordem a ser criada, sendo, buy para compra e sell para venda;

amount Volume da ordem;

price Preço da ordem

Campos:

asset Par da ordem;

currency Sempre BRL;

action Tipo de ordem, sendo, buy para compra ou sell venda;

status Status da ordem, sendo, OPEN para pendente, CANCELED para cancelada e EXECUTED para executada;

amount Volume da ordem;

executedPriceAverage Valor já executado;

executedAmount Volume executado;

dateCreated Data ta criação da ordem;

date Data da requisição no momento absoluto da consulta;

timestamp timestamp retornado no momento absoluto da consulta;

Retorno:


{
    "success": "1",
    "oReturn": 
    [
        {
            "asset": "BTC",
            "currency": "BRL",
            "id": "67229",
            "action": "buy",
            "status": "executed",
            "price": "990,0000000000",
            "amount": "0,00966625",
            "executedPriceAverage": "9,56958750",
            "executedAmount": "0,00966625",
            "dateCreated": "2014-10-09 14:05:13.500",
        }
    ],
    "date": "2014-10-09 14:05:13.400",
    "timestamp": "1412863513"
}

deleteOrders.aspx

Autenticação

Sim

Parâmetros:

id Id da ordem que deseja cancelar;

Campos:

asset Par da ordem;

currency Sempre BRL;

action Tipo de ordem, sendo, buy para compra ou sell venda;

status Status da ordem, sendo, OPEN para pendente, CANCELED para cancelada e EXECUTED para executada;

amount Volume da ordem;

executedpriceaverage Valor já executado;

executedAmount Volume executado;

dateCreated Data ta criação da ordem;

date Data da requisição no momento absoluto da consulta;

timestamp timestamp retornado no momento absoluto da consulta;

Retorno:


{
    "success": "1",
    "oReturn": 
    {
        "asset": "BTC",
        "currency": "BRL",
        "id": "67233",
        "action": "buy",
        "status": "canceled",
        "price": "500,9800000000",
        "amount": "0,01000000",
        "executedPriceAverage": "0,00000000",
        "executedAmount": "0,00000000",
        "dateCreated": "09/10/2014 14:07:52"
    },
    "date": "2014-10-09 14:14:04.543",
    "timestamp": "1412864044"
}

getOrders.aspx

Autenticação

Sim

Parâmetros:

status Status da ordem, sendo, OPEN para pendente, CANCELED para cancelada e EXECUTED para executada;

Campos:

asset Par da ordem;

currency Sempre BRL;

action Tipo de ordem, sendo, buy para compra ou sell venda;

status Status da ordem, sendo, OPEN para pendente, CANCELED para cancelada e EXECUTED para executada;

amount Volume da ordem;

executedPriceAverage Valor já executado;

executedAmount Volume executado;

dateCreated Data ta criação da ordem;

date Data da requisição no momento absoluto da consulta;

timestamp timestamp retornado no momento absoluto da consulta;

Retorno:


{
    "success": "1",
    "oReturn": 
    {
        "asset": "BTC",
        "currency": "BRL",
        "id": "67233",
        "action": "buy",
        "status": "canceled",
        "price": "500,9800000000",
        "amount": "0,01000000",
        "executedPriceAverage": "0,00000000",
        "executedAmount": "0,00000000",
        "dateCreated": "09/10/2014 14:07:52"
    },
    "date": "2014-10-09 14:14:04.543",
    "timestamp": "1412864044"
}

getOrdersId.aspx

Autenticação

Sim

Parâmetros:

id Id da ordem que deseja consultar;

Campos:

asset Par da ordem;

currency Sempre BRL;

action Tipo de ordem, sendo, buy para compra ou sell venda;

status Status da ordem, sendo, OPEN para pendente, CANCELED para cancelada e EXECUTED para executada;

amount Volume da ordem;

executedPriceAverage Valor já executado;

executedAmount Volume executado;

dateCreated Data ta criação da ordem;

date Data da requisição no momento absoluto da consulta;

timestamp timestamp retornado no momento absoluto da consulta;

Retorno:


{
    "success": "1",
    "oReturn": 
    {
        "asset": "BTC",
        "currency": "BRL",
        "id": "67233",
        "action": "buy",
        "status": "canceled",
        "price": "500,9800000000",
        "amount": "0,01000000",
        "executedPriceAverage": "0,00000000",
        "executedAmount": "0,00000000",
        "dateCreated": "09/10/2014 14:07:52"
    },
    "date": "2014-10-09 14:14:04.543",
    "timestamp": "1412864044"
}

orderbook.aspx

Autenticação

Não

Parâmetros:

Não possui

Campos:

asks Ordens de compra disponíveis;

bids Ordens de venda disponíveis;

Retorno:


{
 "asks": [[4955.3000000000,0.01575303][3070.0000000000,0.01990000]],
 "bids": [[956.7200000000,0.00055518][955.8600000000,0.00014486]]
}

orderbook_litecoin.aspx

Autenticação

Não

Parâmetros:

Não possui

Campos:

asks Ordens de compra disponíveis;

bids Ordens de venda disponíveis;

Retorno:


{
    "asks": [[4955.3000000000,0.01575303][3070.0000000000,0.01990000]],
    "bids": [[956.7000000000,0.00007620][955.8600000000,0.00014486]]
}

ticker.aspx

Autenticação

Não

Parâmetros:

Não possui

Campos:

high Maior preço negociado;

low Menor preço negociado;

vol Volume total negociado;

last Último preço negociado;

buy Preço da ordem de compra;

sell Preço da ordem de venda;

date Data e hora da requisição;

Retorno:


{
    "ticker":
    {
        "high": "990.00",
        "low": "905.01",
        "vol": "58.16484697",
        "last": "955.04",
        "buy": "954.7900000000",
        "sell": "982.4800000000",
        "date": "1412878640"
    }
}

ticker_litecoin.aspx

Autenticação

Não

Parâmetros:

Não possui

Campos:

high Maior preço negociado;

low Menor preço negociado;

vol Volume total negociado;

last Último preço negociado;

buy Preço da ordem de compra;

sell Preço da ordem de venda;

date Data e hora da requisição;

Retorno:


{
    "ticker":
    {
        "high": "0.00",
        "low": "0.00",
        "vol": "0.00000000",
        "last": "10.00",
        "buy": "9.0000000000",
        "sell": "12.0000000000",
        "date": "1412878746"
    }
}

trades.aspx

Autenticação

Não

Parâmetros:

timestamp Para exbir as negociações realizadas apartir da determinada data e hora em UNIX Time;

currency Definir o par desejado, sendo BTC para Bitcoin e LTC para Litecoin;

tid Exibe os registros a partir de um determinado ID; (id >= tid)

Campos:

date Data hora em UNIX Time da execução da ordem;

price Preço da ordem executada;

amount Volume da ordem executada;

tid Identificação da ordem executada;

currency Moeda, sendo BTC para Bitcoin e LTC para Litecoin;

Retorno:


[
    {
        "date": 1412861436,
        "price": 980.28,
        "amount": 0.00992380,
        "tid": 25525,
        "type": "buy",
        "currency": "BTC"
    },
    {
        "date": 1412862865,
        "price": 977.21,
        "amount": 0.00065518,
        "tid": 25526,
        "type": "buy",
        "currency": "BTC"
    },
    {
        "date": 1412862865,
        "price": 977.95,
        "amount": 0.00005507,
        "tid": 25527,
        "type": "buy",
        "currency": "BTC"
    }
]

