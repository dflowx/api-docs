# Dflow Open Api

## Endpoint = https://api.dflowx.com/v1/

## 1. API LIST

-   (GET) /v1/order/list - Obtain All Order history

-   (GET) /v1/order/complete/list - Obtain All Trade History

-   (POST) /v1/order/cancel - Cancel Order

-   (GET) /v1/market/list - Obtain Trade Symbol Info

-   (POST) /v1/order/create - Create Order

-   (GET) /v1/market/chart - Obtain Market Record

-   (GET) /v1/market/ticker - Obtain Ticker Data

-   (GET) /v1/order/recent/list - Complete Trade History

-   (GET) /v1/market/price - Obtain Market Data

-   (GET) /v1/market/recent - Obtain Market Data

-   (GET) /v1/order/pending/list - Obtain The Most Recent Order Info

-   (GET) /v1/order - Obtain Specific Order Info

-   (GET) /v1/user/accounts - Obtain Account Info

## 2. Basic rules

### Signing

Order the parameters in alphabetical order with respect to the keyvalue and generate String. Then, sign=MD5(string+secretKey).  

> **Important**
>
> If the value of the parameter is NULL, that is, it is not written to the alphabet string temporary signature alphabet string

**example (/v1/order/create).**

    A)Params：
    {
        api_key = k3j1n2kcee32asx2255fdcbffp12k1n;
        price = 200;
        side = BUY;
        symbol = ethusdt;
        time = 1558299834409;
        type = 1;
        volume = 10;
    }

    B)Generated String：
    string = api_keybkdfo2019sj12k1255fdcbb1332aecprice200sideBUYsymbolethusdttime1558299834409type1volume11

    C)Hashing :
    sign=MD5(string + secretKey)

### Content Type

-   content-type : application/x-www-formurlencoded

## 3.Error Code

| CODE  | Description  | Description |
|---|---|---|
| 0  |  success |   |
| 5  | Order failed  |   |
| 6  | The amount is smaller than the minimum  |   |
| 7  | The amount is bigger than the maximum  |   |
| 8  | Cancel order failed  |   |
| 9  | Trade is locked  |   |
| 13  | System error. Please contact the support  |   |
| 19  | Not enough balance  |   |
| 22  | The trade doesn’t exit  |   |
| 23  | Amount parameter missing  |   |
| 24  | Price parameter missing  |   |
| 1001  | System error  |   |
| 1004  | Illegal request parameter  |   |
| 1005  | Illegal Sign  |   |
| 1007  | Illegal IP  |   |
| 1102  | Incorrect currency  |   |
| 1103  | Incorrect security password  |   |
| 1104  | Withdrawal is locked  |   |
| 1105  | Not enough balance  |   |
| 1120  | User doesn’t exist  |   |
| 1123  | The phone number has been registered already  |   |
| 1124  | The email has been registered already  |   |
| 1125  | Admin has locked the account  |   |
| 1132  | Unauthorized  |   |
| 1133  | Deposit fail  |   |
| 1134  | Withdrawal Fail  |   |

## 4-1.(GET) /v1/order/list - Obtain All Order history

### request

| Parameter  | Type  | Desc |
|---|---|---|
| symbol  |  Required | Currency pair (e.g. btc_usdt)  |
| page  |  Optional | Page  |
| api_key  |  Required | api_key  |
| time  |  Required | timestamp  |
| sign  |  Required | sign  |


### response
| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |
**Example data.**

    {
      "data": {
        "order_list": [
          {
            "created_at": 1527333468000,
            "filled_volume": "0.00110000",
            "volume": "0.001",
            "trade_currency": "btc",
            "id": 112864,
            "remain_volume": "0.00000001",
            "price": "0.07979924",
            "filled_trades": [
              {
                "fee_volume": "0.00000000",
                "volume": "0.001",
                "time": 1527333467000,
                "id": 56341,
                "price": "0.07979924",
                "trade_price": "0.00007979",
                "fee_symbol": "ETH",
                "type": "BUY"
              }
            ],
            "base_currency": "eth",
            "status": 2,
            "price": "0.00007968",
            "side": "BUY",
            "status_msg": "successcess",
            "avg_price": "0.07979871",
            "side_msg": "BUY"
          }
        ],
        "total": 112852,
        "pageSize" : 30
      },
      "code": "0",
      "msg": "success"
    }

## 4-2. (GET)  /v1/order/complete/list - Obtain All Trade History

### request
| Parameter  | Type  | Desc |
|---|---|---|
| symbol  |  Required | Currency pair (e.g. btc_usdt)  |
| page  |  Optional | Page  |
| api_key  |  Required | api_key  |
| time  |  Required | timestamp  |
| sign  |  Required | sign  |


### response
| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": {
        "total": 2,
        "pageSize" : 30
        "list": [
          {
            "volume": "0.186",
            "side": "SELL",
            "fee_symbol": "BTC",
            "price": "0.04400000",
            "fee_volume": "0.00000820",
            "time": 1535968300000,
            "trade_price": "0.00820028",
            "id": 140,
            "bid_id": 282,
            "ask_id": 281
          },
          {
            "volume": "0.186",
            "side": "BUY",
            "fee_symbol": "ETH",
            "price": "0.04400000",
            "fee_volume": "0.00018637",
            "time": 1535968300000,
            "trade_price": "0.00820028",
            "id": 140,
            "bid_id": 282,
            "ask_id": 281
          }
        ]
      }
    }

## 4-3. (POST) /v1/order/cancel  - Cancel Order

### request

| Parameter  | Type  | Desc |
|---|---|---|
| order_id  |  Required | 주문 ID  |
| symbol  |  Optional | Currency pair (e.g. btc_usdt)  |
| api_key  |  Required | api_key  |
| time  |  Required | timestamp  |
| sign  |  Required | sign  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |

## 4-4. (GET)  /v1/market/list  - Obtain Trade Symbol Info

-   No signature

### request

 | Parameter  | Type  | Desc |
 |---|---|---|
 |   |   |   |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": [
        {
          "symbol": "btcusdt",
          "count_coin": "usdt",
          "amount_precision": 6,
          "base_coin": "btc",
          "price_precision": 2
        },
        {
          "symbol": "btcusdt",
          "count_coin": "usdt",
          "amount_precision": 3,
          "base_coin": "btc",
          "price_precision": 4
        }
      ]
    }

## 4-5. (POST) /v1/order/create - Create Order

### request

| Parameter  | Type  | Desc |
|---|---|---|
| side  |  Required | "BUY", "SELL"  |
| type  |  Required | 1: Limit, 2: Market  |
| volume  |  Required | Total order volume  |
| price  |  Optional | Required if type:1  |
| symbol  |  Required | Currency pair (e.g. btc_usdt)  |
| api_key  |  Required | api_key  |
| time  |  Required | timestamp  |
| sign  |  Required | sign  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |

## 4-6. (GET) /v1/market/chart - Obtain Market Record

-   No signature

### request

| Parameter  | Type  | Desc |
|---|---|---|
| symbol  |  Required | Currency pair (e.g. btcusdt)  |
| period  |  Required | Minutes. 1hour: 60  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": [
        [
          time : 1536001200,    
          open : 271.93,            
          high : 271.93,            
          low : 271.93,            
          close : 271.93,             
          volume : 0             
        ],
        [
          time : 1536001233,    
          open : 71.93,            
          high : 71.93,            
          low : 71.93,            
          close : 71.93,             
          volume : 1            
        ]
      ]
    }

## 4-7. (GET) /v1/market/ticker - Obtain Ticker Data

-   No signature

### request

| Parameter  | Type  | Desc |
|---|---|---|
| symbol  |  Required | Currency pair (e.g. btcusdt)  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": {
        "ethusdt": {
          "high": 1100,
          "vol": 45,
          "last": 790,
          "low": 11,
          "buy": "800.00",
          "sell": "900.00",
          "time": 1531217396533
        }
      }
    }

## 4-8. (GET) /v1/order/recent/list  - Complete Trade History

-   No signature

### request

| Parameter  | Type  | Desc |
|---|---|---|
| symbol  |  Required | Currency pair (e.g. btcusdt)  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": [
        {
          "amount": 0.01957,
          "price": 790,
          "id": 1665,
          "type": "buy"
        },
        {
          "amount": 0.11336,
          "price": 790,
          "id": 1664,
          "type": "sell"
        }
      ]
    }

## 4-9. (GET) /v1/market/price - Obtain Market Depth Data

-   No signature

### request

| Parameter  | Type  | Desc |
|---|---|---|
| symbol  |  Required | Currency pair (e.g. btcusdt)  |
| type  |  Required | Depth level: step0, step1, step2 (finest)  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": {
        "ticker": {
          "asks": [
            [ "900", 0.02781 ],            // price, volume
            [ "1000", 0.33263 ]
          ],
          "bids": [
            [ "800", 0.0995 ]
          ],
          "time": 1531217396533
        }
      }
    }

## 4-10. (GET) /v1/market/recent - Obtain Market Data

### request

| Parameter  | Type  | Desc |
|---|---|---|
| api_key  |  Required | api_key  |
| time  |  Required | timestamp  |
| sign  |  Required | sign  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": {
        "qtumbtc": 0.000641,
        "btcusdt": 6439.04,
        "ethbtc": 0.044,
        "bchbtc": 0.08094,
        "bchusdt": 516.89,
        "qtumusdt": 4.041,
        "ethusdt": 790
      }
    }

## 4-11. (GET)  /v1/order/pending/list - Obtain The Most Recent Order Info

### request

| Parameter  | Type  | Desc |
|---|---|---|
| symbol  |  Required | Currency pair (e.g. btcusdt)  |
| page  |  Optional | Page  |
| api_key  |  Required | api_key  |
| time  |  Required | timestamp  |
| sign  |  Required | sign  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": {
        "total": 2,
        "pageSize": 30,
        "list": [
          {
            "side": "SELL",
            "total_price": "6976.02",
            "created_at": 1536118132923,
            "avg_price": "0.00000000",
            "trade_currency": "usdt",
            "side_msg": "SELL",
            "volume": "0.99657500",
            "price": "7000.00",
            "status_msg": "Unfilled",
            "filled_volume": "0.00000000",
            "id": 263,
            "remain_volume": "0.99657500",
            "base_currency": "btc",
            "filled_trades": [],
            "status": 1
          },
          {
            "side": "BUY",
            "total_price": "24.44",
            "created_at": 1536118089957,
            "avg_price": "0.00000000",
            "trade_currency": "usdt",
            "volume": "0.00379800",
            "price": "6436.00",
            "source_msg": "WEB",
            "status_msg": "Unfilled",
            "filled_volume": "0.00000000",
            "id": 262,
            "remain_volume": "0.00379800",
            "trade_currency": "btc",
            "filled_trades": [],
            "status": 1
          }
        ]
      }
    }

## 4-12. (GET) /v1/order - Obtain Specific Order Info

### request

| Parameter  | Type  | Desc |
|---|---|---|
| order_id  |  Required | order id  |
| symbol  |  Required | Currency pair (e.g. btcusdt)  |
| api_key  |  Required | api_key  |
| time  |  Required | timestamp  |
| sign  |  Required | sign  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |   |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": {
        "trade": [
          {
            "volume": "0.00900000",
            "fee_symbol": "USDT",
            "price": "6431.63",
            "fee_volume": "0.05",
            "time": 1534991068000,
            "trade_price": "57.88",
            "id": 55,
            "type": "SELL"
          },
          {
            "volume": "0.00100000",
            "fee_symbol": "USDT",
            "price": "6431.63",
            "fee_volume": "0.00",
            "time": 1534991089000,
            "trade_price": "6.43",
            "id": 56,
            "type": "SELL"
          }
        ],
        "order_info": {
          "side": "SELL",
          "total_price": "64.31",
          "created_at": 1534991067588,
          "avg_price": "6431.63",
          "trade_currency": "usdt",
          "source": 3,
          "type": 1,
          "side_msg": "SELL",
          "volume": "0.01000000",
          "price": "6431.63",
          "status_msg": "success",
          "filled_volume": "0.01000000",
          "id": 100,
          "remain_volume": "0.00000000",
          "base_currency": "btc",
          "tradeList": [
            {
              "volume": "0.00900000",
              "feeCoin": "USDT",
              "price": "6431.63",
              "fee": "0.05",
              "ctime": 1534991068000,
              "deal_price": "57.88",
              "id": 55,
              "type": "SELL"
            },
            {
              "volume": "0.00100000",
              "fee_symbol": "USDT",
              "price": "6431.63",
              "fee_volume": "0.00",
              "time": 1534991089000,
              "trade_price": "6.43",
              "id": 56,
              "type": "SELL"
            }
          ],
          "status": 2
        }
      }
    }

## 4-13. (GET)  /v1/user/accounts  - Obtain Account Info

### request

| Parameter  | Type  | Desc |
|---|---|---|
| api_key  |  Required | api_key  |
| time  |  Required | timestamp  |
| sign  |  Required | sign  |

### response

| Field  | Example  | MISC |
|---|---|---|
| code  |  0 | code>0:Fail  |
| msg  |  "success" |  |
| data  |  Please refer to the below | Page  |

**Example data.**

    {
      "code": "0",
      "msg": "success",
      "data": {
        "total_asset": "20052.32902812",
        "balance": [
          {
            "available": "8.77629030",
            "in_use": "1.85091253",
            "asset": "btc"
          },
          {
            "available": "331032.69901617",
            "in_use": "69751.96400000",
            "asset": "eth"
          }
        ]
      }
    }
