[toc]

# VirgoX API

* The RESTful API base URL is: **https://www.virgox.net**
* All the responses are formatted in JSON.
* For API connection, please contact customer service to provide you IP address

----

## **Signature Rule** 

Public endpoints do not require a sign, otherwise one must have a sign in requests to all endpoints that require it. `apiKey`, and `sign` are mandatory for private endpoints，all the parameters except `sign` are required for generating the signature.

| Parameter |  TYPE  | Mandatory |      note      |
| :-------: | :----: | :-------: | :------------: |
|  apiKey   | string |     Y     |  Your apiKey   |
|   sign    | string |     Y     | Your signature |

**Signature Rule** 

* 1.Set parameters (except ‘sign’) as a dictionary ordered by set parameters names.

```json
{
    "apiKey":"AAAAA",
    "apiSecret":"BBBBB",
    "category":"1",
    "price":"9000.1",
    "qty":"1.2",
    "symbol":"BTC/CAD",
    "type":"1"
}
```

* Concatenate values of these parameters after sorting. You will have: AAAAABBBBB19000.11.2BTC/CAD1。

* Apply MD5 encryption to the series above, you will have your sign: b60743ad70bad7d1fc47777c0d58604e。

* Set the series above (your sign) as the value of the sign parameter to complete the request. 


## **Candlestick charts Data**

* GET `/apis/api/market/history/kline`

**Request Parameters **

| Parameter |  TYPE  | Mandatory |                             note                             |
| :-------: | :----: | :-------: | :----------------------------------------------------------: |
|  symbol   | String |     Y     |  Traded currency pair -- separated by /.  Such as ETH/USDT.  |
|  period   |  Int   |     Y     | Frequency of candles, in minutes. Example: period=1 – 1 minute, period=60 – 1 hour, period=240 – 4 hours, period=10080 – 1 week. |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "success":true,
    "data":[
        {
            "id":1,
            "marketId":21,
            "open":1,
            "high":1,
            "low":1,
            "close":1,
            "qty":1,
            "createTime":1557211356000
        }
    ]
}
```

**Return Parameters**

| Parameter  |  type   |                  note                   |
| :--------: | :-----: | :-------------------------------------: |
|     id     |   Int   |            id of candlestick            |
|  marketId  |   Int   |              id of market               |
|    low     | Decimal |  lowest price for the requested period  |
|    high    | Decimal | highest price for the requested period  |
|   close    | Decimal |  close price for the requested period   |
|    open    | Decimal |   open price for the requested period   |
|    qty     | Decimal | trading volume for the requested period |
| createTime |  Long   |           creation timestamp            |


## **Ticker Data**

* GET `/apis/api/market/detail/merged`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |                            note                            |
| :-------: | :----: | :-------: | :--------------------------------------------------------: |
|  symbol   | String |     Y     | Traded currency pair -- separated by /.  Such as ETH/USDT. |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":{
        "volume":85.98,
        "symbol":"BTC/USDT",
        "high":8889.87,
        "last":8794.39,
        "low":8709.73,
        "buy":8710.99,
        "sell":8840.69,
        "id":91,
        "changeRate":"+0.08%",
        "open":8786.49
    },
    "success":true
}
```

**Return Parameters**

| Parameter  |  type   |          note          |
| :--------: | :-----: | :--------------------: |
|     id     |   Int   |       market id        |
|    low     | Decimal |      lowest price      |
|    high    | Decimal |     highest price      |
|    last    | Decimal |       open price       |
|    open    | Decimal |      latest price      |
|    sell    | Decimal |    lowest ask price    |
|    buy     | Decimal |   highest bid price    |
|   volume   | Decimal | volume (by quote unit) |
|   symbol   | String  |  traded currency pair  |
| changeRate | Decimal |    change in price     |


## **Snapshot of all Currency Pairs**

* GET `/apis/api/market/tickers`

**Request Parameters** 

| Parameter | TYPE | Mandatory | note |
| :-------: | :--: | :-------: | :--: |
|   none    | none |   none    | none |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":[
        {
            "volume":83.1,
            "symbol":"BTC/USDT",
            "high":8889.87,
            "last":8787.47,
            "low":8709.73,
            "buy":8714.19,
            "sell":8848.52,
            "id":91,
            "changeRate":"+0.01%",
            "open":8786.49
        },
        {
            "volume":0,
            "symbol":"ETH/USDT",
            "high":0,
            "last":213.82,
            "low":0,
            "buy":212.09,
            "sell":214.9,
            "id":90,
            "changeRate":"+0.00%",
            "open":0
        }
    ],
    "success":true
}
```

**Return Parameters**

| Parameter  |  type   |          note          |
| :--------: | :-----: | :--------------------: |
|     id     |   Int   |       market id        |
|    low     | Decimal |      lowest price      |
|    high    | Decimal |     highest price      |
|    last    | Decimal |       open price       |
|    open    | Decimal |      latest price      |
|   volume   | Decimal | volume (by quote unit) |
|   symbol   | String  |  traded currency pair  |
| changeRate | Decimal |    change in price     |
|    sell    | Decimal |    lowest ask price    |
|    buy     |  Long   |   highest bid price    |


## **Market Depth**

* GET `/apis/api/market/depth`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |                            note                            |
| :-------: | :----: | :-------: | :--------------------------------------------------------: |
|  symbol   | String |     Y     | Traded currency pair -- separated by /.  Such as ETH/USDT. |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":{
        "asks":[
            {
                "id":"3229af464d014b588e4d12b288d96c9e",
                "marketId":8764.78,
                "price":8764.78,
                "qty":0.084783,
                "volume":743.10434274
            },
            {
                "id":"6f93f30c1289441aa5756affe33c849b",
                "marketId":8764.78,
                "price":8765.88,
                "qty":0.050587,
                "volume":443.43957156
            }
        ],
        "ts":1590401000781
    },
    "success":true
}
```

**Return Parameters**

| Parameter |  type   |                  note                  |
| :-------: | :-----: | :------------------------------------: |
|    id     | String  |          id of a market depth          |
| marketId  |   Int   |               market id                |
|   price   | Decimal |                 price                  |
|  volume   | Decimal | total market value at this price level |
|    qty    | Decimal |      quantity at this price level      |


## **Latest Transactions**

* GET `/apis/api/market/trade`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |                            note                            |
| :-------: | :----: | :-------: | :--------------------------------------------------------: |
|  symbol   | String |     Y     | Traded currency pair -- separated by /.  Such as ETH/USDT. |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":{
        "tradeList":[
            {
                "id":794780,
                "qty":0.060999,
                "price":8868.13,
                "type":2,
                "createTime":1590399172000,
                "doublePrice":8868.13
            },
            {
                "id":794776,
                "qty":0.022285,
                "price":8870.43,
                "type":2,
                "createTime":1590399158000,
                "doublePrice":8870.43
            }
        ],
        "ts":1590399185283
    },
    "success":true
}
```

**Return Parameters**

|  Parameter  |  type   |                     note                     |
| :---------: | :-----: | :------------------------------------------: |
|     id      | String  |                transaction id                |
|    price    | Decimal |               transacted price               |
|     qty     | Decimal |        quantity of assets transacted         |
|    type     |   Int   | direction of transactions, 1 - buy, 2 - sell |
| createTime  |  Long   |            transaction timestamp             |
| doublePrice | double  |               transacted price               |


## **Place Order**

* POST `/apis/api/member/addOrder`
  ***(Note：Users need turn off trading password for placing order by API)***

**Request Parameters** 

| Parameter |  TYPE   | Mandatory |                             note                             |
| :-------: | :-----: | :-------: | :----------------------------------------------------------: |
|  apiKey   | String  |     Y     |                       client’s api key                       |
|   sign    | String  |     Y     |                          signature                           |
|  symbol   | String  |     Y     |  Traded currency pair -- separated by /.  Such as ETH/USDT.  |
| category  |   Int   |     Y     |                 Order type, 1 Limit 2 Market                 |
|   type    |   Int   |     Y     |                         1 Buy 2 Sell                         |
|   price   | Decimal |     N     |               price, mandatory when category=1               |
|   total   | Decimal |     N     |      total amount, mandatory when category=2 and type=1      |
|    qty    | Decimal |     N     | Quantity, mandatory when category=1 or category=2 and type = 2 |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":{
        "orderId":15
    },
    "success":true
}
```

**Return Parameters**

| Parameter |  type  |   note   |
| :-------: | :----: | :------: |
|  orderId  | String | Order id |


## **Cancel Order**

* GET `/apis/api/member/cancelOrder`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |            note             |
| :-------: | :----: | :-------: | :-------------------------: |
|  apiKey   | String |     Y     |      client’s api key       |
|   sign    | String |     Y     |          signature          |
|    id     | String |     Y     | id of order to be cancelled |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":"OrderCancelled!",
    "success":true
}
```

**Return Parameters**

| Parameter | type | note |
| :-------: | :--: | :--: |
|   none    | none | none |


## **Account Information**

* GET `/apis/api/member/accounts`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |       note       |
| :-------: | :----: | :-------: | :--------------: |
|  apiKey   | String |     Y     | client’s api key |
|   sign    | String |     Y     |    signature     |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":[
        {
            "total":0,
            "balance":0,
            "coinName":"ETH",
            "freezingBalance":0
        },
        {
            "total":0,
            "balance":0,
            "coinName":"BTC",
            "freezingBalance":0
        },
        {
            "total":10000,
            "balance":10000,
            "coinName":"USDT",
            "freezingBalance":0
        },
        {
            "total":0,
            "balance":0,
            "coinName":"PAX",
            "freezingBalance":0
        },
        {
            "total":0,
            "balance":0,
            "coinName":"USDC",
            "freezingBalance":0
        }
    ],
    "success":true
}
```

**Return Parameters**

|    Parameter    |  type   |                  note                  |
| :-------------: | :-----: | :------------------------------------: |
|     balance     | Decimal |           available balance            |
| freezingBalance | Decimal | frozen balance for margin requirements |
|      total      | Decimal |             total balance              |
|    coinName     | String  |             name of a coin             |

## **Order Lookup**

* GET `/apis/api/member/queryOrder`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |                             note                             |
| :-------: | :----: | :-------: | :----------------------------------------------------------: |
|  apiKey   | String |     Y     |                       client’s api key                       |
|   sign    | String |     Y     |                          signature                           |
|  symbol   | String |     Y     |  Traded currency pair -- separated by /.  Such as ETH/USDT   |
|  status   |  Int   |     Y     | status of an order, -1 – order cancelled, 0 – order placed, 1 – fill pending, 2 – fill in progress, 3 – order filled |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":[
        {
            "createTime":1593602042000,
            "price":9224.18,
            "qty":0.079137,
            "tradeQty":0,
            "id":44788514,
            "type":1,
            "direction":2,
            "status":0
        },
        {
            "createTime":1593602042000,
            "price":9105.72,
            "qty":0.083102,
            "tradeQty":0,
            "id":44788513,
            "type":1,
            "direction":1,
            "status":1
        }
    ],
    "success":true
}
```

**Return Parameters**

| Parameter  |  type   |                             note                             |
| :--------: | :-----: | :----------------------------------------------------------: |
|     id     |   Int   |                           order id                           |
|    type    |   Int   |               type of order, 1 limit, 2 market               |
| direction  |   Int   |              direction of order, 1 buy, 2 sell               |
|   price    | Decimal |                         order price                          |
|    qty     | Decimal |                        order quantity                        |
|  tradeQty  | Decimal |                       filled quantity                        |
|   status   |   Int   | status of an order, -1 – order cancelled, 0 – order placed, 1 – fill pending, 2 – fill in progress, 3 – order filled |
| createTime |  Long   |                   Order created Timestamp                    |


## **Transaction History Lookup**

* GET `/apis/api/member/queryTrade`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |                           note                            |
| :-------: | :----: | :-------: | :-------------------------------------------------------: |
|  apiKey   | String |     Y     |                     client’s api key                      |
|   sign    | String |     Y     |                         signature                         |
|  symbol   | String |     Y     | Traded currency pair -- separated by /.  Such as ETH/USDT |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":[
        {
            "id":1,
            "amount":12,
            "qty":1,
            "price":12,
            "type":"buy",
            "createTime":"2021-02-22 11:21:07",
            "createTimeMs":1613964067000
        }
    ],
    "success":true
}
```

**Return Parameters**

|  Parameter   |  type   |              note               |
| :----------: | :-----: | :-----------------------------: |
|      id      |   Int   |         transaction id          |
|     qty      | Decimal |            quantity             |
|    amount    | Decimal |    total price paid/received    |
|     type     | String  |  direction of order, buy/sell   |
|    price     | Decimal |       average fill price        |
| createTimeMs |  Long   | transacted time in milliseconds |
|  createTime  | String  |         transacted time         |


## **Market Information**

* GET `/apis/api/marketInfo`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |                           note                            |
| :-------: | :----: | :-------: | :-------------------------------------------------------: |
|  symbol   | String |     N     | Traded currency pair -- separated by /.  Such as ETH/USDT |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":[
        {
            "id":91,
            "marketName":"BTC/USDT",
            "categoryCoin":"USDT",
            "marketCoin":"BTC",
            "minTotal":1,
            "maxTotal":10000,
            "minQty":0.0001,
            "maxQty":0.31,
            "priceDecimals":2,
            "qtyDecimals":6
        }
    ],
    "success":true
}
```

**Return Parameters**

|  Parameter   |  type   |           note            |
| :----------: | :-----: | :-----------------------: |
|      id      |   Int   |         Market id         |
|  marketName  | String  |        Market name        |
| categoryCoin | String  |        quote coin         |
|  marketCoin  | String  |         base coin         |
|   minTotal   | Decimal |  Minimum tradable total   |
|   maxTotal   | Decimal |  Maximum tradable total   |
|    minQty    | Decimal | Minimum tradable quantity |
|    maxQty    | Decimal | Maximum tradable quantity |
| priceDecimal | Decimal |      Price precision      |
|  qtyDecimal  | Decimal |    Quantity precision     |

## **Order History Lookup**

* GET `/apis/api/member/queryOrderInfo`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |                           note                            |
| :-------: | :----: | :-------: | :-------------------------------------------------------: |
|  apikey   | String |     Y     |                          apiKey                           |
|   sign    | String |     Y     |                         signature                         |
|  orderId  | String |     Y     | Traded currency pair -- separated by /.  Such as ETH/USDT |

**Return Example**

```json
{
    "code":0,
    "msg":"success",
    "data":{
        "id":"20405197",
        "direction":1,
        "type":1,
        "price":0.972893,
        "qty":273.4,
        "tradeQty":0,
        "status":1,
        "detail":[
            {
                "amount":663.3669056,
                "create_time":1599883383000,
                "price":10351.36,
                "qty":0.064085,
                "fee":0,
                "feeCoinName":"USDT",
                "id":2,
                "createTimeMs":1599883383000
            }
        ],
        "createTime":1604687659000
    },
    "success":true
}
```

**Return Parameters**

|  Parameter   |  type   |               note                |
| :----------: | :-----: | :-------------------------------: |
|      id      |   Int   |             Order Id              |
|  direction   |   Int   | direction of order, 1 buy, 2 sell |
|     type     |   Int   | type of order, 1 limit, 2 market  |
|    price     | Decimal |            Order price            |
|     qty      | Decimal |          Order quantity           |
|   tradeQty   | Decimal |          Filled quantity          |
|    status    |   Int   |           Order status            |
|    detail    | Object  |        Transaction details        |
|    amount    | Decimal |           Filled amount           |
|  createTime  |  Long   |         Filled timestamp          |
|    price     | Decimal |           Filled price            |
|     qty      | Decimal |          Filled quantity          |
|     fee      | Decimal |          Transaction fee          |
| feeCoinName  | String  |      Fee’s settled coin name      |
|      id      | String  |          Transaction Id           |
| createTimeMs |  Long   |    Order created ms timestamp     |


## **Deposit Record Lookup**

* POST `/apis/api/member/rechargeRecords`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |   note    |
| :-------: | :----: | :-------: | :-------: |
|  apikey   | String |     Y     |  apiKey   |
|   sign    | String |     Y     | signature |
| coinName  | String |     N     | coin name |

**Return Example**

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "total": 3,
        "list": [
            {
                "coinType": 4,
                "blockConfirm": 0,
                "memo": null,
                "txId": null,
                "remark": null,
                "updateTime": 1612775730,
                "type": 1,
                "toAddress": null,
                "coinId": 10,
                "createTime": 1612775702,
                "browser": "https://www.omniexplorer.info/tx/",
                "qty": 100000.000000000000000,
                "fromAddress": null,
                "id": 3,
                "coinName": "USDT",
                "blockConfirmTotal": 2,
                "status": "completed"
            },
            {
                "coinType": 2,
                "blockConfirm": 0,
                "memo": null,
                "txId": null,
                "remark": null,
                "updateTime": 1612775730,
                "type": 1,
                "toAddress": null,
                "coinId": 2,
                "createTime": 1612775702,
                "browser": "https://btc.com/",
                "qty": 100.000000000000000,
                "fromAddress": null,
                "id": 2,
                "coinName": "BTC",
                "blockConfirmTotal": 2,
                "status": "completed"
            }
        ],
        "pageNum": 1,
        "pageSize": 10,
        "size": 3,
        "startRow": 1,
        "endRow": 3,
        "pages": 1,
        "prePage": 0,
        "nextPage": 0,
        "isFirstPage": true,
        "isLastPage": true,
        "hasPreviousPage": false,
        "hasNextPage": false,
        "navigatePages": 8,
        "navigatepageNums": [
            1
        ],
        "navigateFirstPage": 1,
        "navigateLastPage": 1
    },
    "success": true
}
```

**Return Parameters**

|     Parameter     |  type   |                     note                      |
| :---------------: | :-----: | :-------------------------------------------: |
|        id         |   Int   |               deposit record id               |
|     coinName      | String  |                   coin name                   |
|      status       |   Int   | deposit status, processing, completed, failed |
|   blockConfirm    |   Int   |            number of confirmations            |
| blockConfirmTotal |   Int   |       required number of confirmations        |
|       memo        | Stirng  |                     memo                      |
|       txId        | String  |               transaction hash                |
|    fromAddress    | String  |                 from address                  |
|     toAddress     | String  |                  to address                   |
|        qty        | Decimal |               deposit quantity                |
|      browser      | String  |              blockchain explorer              |
|    createTime     |  Long   |           creation timestamp in ms            |


## **Withdraw Record Lookup**

* POST `/apis/api/member/withdrawRecords`

**Request Parameters** 

| Parameter |  TYPE  | Mandatory |   note    |
| :-------: | :----: | :-------: | :-------: |
|  apikey   | String |     Y     |  apiKey   |
|   sign    | String |     Y     | signature |
| coinName  | String |     N     | coin name |

**Return Example**

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "total": 1,
        "list": [
            {
                "coinType": 3,
                "fee": 5.000000000000000000,
                "memo": null,
                "txId": null,
                "updateTime": 1616990583,
                "toAddress": "0x51e7122ccf2d1dad8328720276858e3525392877",
                "coinId": 20,
                "createTime": 1612878285,
                "browser": "https://eth.btc.com/txinfo/",
                "qty": 2900.000000000000000000,
                "fromAddress": null,
                "id": 2,
                "coinName": "USDT",
                "status": "processing"
            }
        ],
        "pageNum": 1,
        "pageSize": 10,
        "size": 1,
        "startRow": 1,
        "endRow": 1,
        "pages": 1,
        "prePage": 0,
        "nextPage": 0,
        "isFirstPage": true,
        "isLastPage": true,
        "hasPreviousPage": false,
        "hasNextPage": false,
        "navigatePages": 8,
        "navigatepageNums": [
            1
        ],
        "navigateFirstPage": 1,
        "navigateLastPage": 1
    },
    "success": true
}
```

**Return Parameters**

| Parameter  |  type   |                      note                      |
| :--------: | :-----: | :--------------------------------------------: |
|     id     |   Int   |               withdraw record id               |
|  coinName  | String  |                   coin name                    |
|   status   |   Int   | withdraw status, processing, completed, failed |
|    memo    | Stirng  |                      memo                      |
|    txId    | String  |                transaction hash                |
| toAddress  | String  |                   to address                   |
|    qty     | Decimal |               withdraw quantity                |
|    fee     | Decimal |                  withdraw fee                  |
|  browser   | String  |              blockchain explorer               |
| createTime |  Long   |            creation timestamp in ms            |
