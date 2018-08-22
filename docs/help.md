# TomoAPI
Tomo API is service connect 

## Features
* Get list tokens ERC20 from address.
* Get price coin or ERC20 tokens from CoinmacketCap
* Get history transaction frome trust ray(other server connected RPCServer)  

BaseURL: http://45.117.82.104:8003





## List tokens ERC20 from an Address

List all tokens erc20 from address

 * @api {post} /tokens
 * @apiVersion 0.1.0
 * @apiName GetTokens
 * @apiGroup Tokens
 * @apiPermission none
 *
 * @apiSampleRequest off
 *
 * @apiParam (Request body) {String[]} networkIndex Array of addresses as a string
 * @apiParam (Request body) {String[]} address Address

### Request:
```
POST : http://45.117.82.104:8003/tokens
```
### Header:
```
Content-Type: application/json
```
 
 
### Param (Request body) raw :
 ```
   {
     "60": ["0xac4df82fe37ea2187bc8c011a23d743b4f39019a"]
   }
 ```
 
### SuccessExample {json} Sucess-Response:
    HtTPS 200 OK


 ```
   {
   "docs": [
        {
           "balance": "0",
            "contract": {
                "contract": "0xf4eced2f682ce333f96f2d8966c613ded8fc95dd",
               "address": "0xf4eced2f682ce333f96f2d8966c613ded8fc95dd",
                "name": "MistCoin",
                 "decimals": 2,
                "symbol": "MC",
                "coin": 60,
                "type": "ERC20"
            }
        },
        {
           "balance": "0",
            "contract": {
                "contract": "0x3111c94b9243a8a99d5a867e00609900e437e2c0",
               "address": "0x3111c94b9243a8a99d5a867e00609900e437e2c0",
                "name": "TEST",
               "decimals": 18,
                "symbol": "TEST",
                "coin": 178,
                "type": "ERC20"
            }
         }
    ]
  }
 ```




## Get Prices
* @api {post} /prices
* @apiVersion 0.1.0
* @apiName GetTokenPrices
* @apiGroup Tokens
* @apiPermission none
* @apiExample {curl} Example usage
* curl -X POST -S -H 'Content-Type: application/json' -d '{"currency":"USD","tokens":[{"contract":"0x1d462414fe14cf489c7a21cac78509f4bf8cd7c0","symbol":"CAN"}]}'
* @apiParam {String} currency="USD" For valid fiat currency values refer to [https://coinmarketcap.com/api/](https://coinmarketcap.com/api/) . Price updates every 5 minutes.
* @apiParam {Object[]} tokens Token object
* @apiParam {String} tokens.contract Smart contract address
* @apiParam {String} tokens.symbol Smart contract symbol
 
### Request:
```
POST : http://45.117.82.104:8003/price
```
### Header:
```
Content-Type: application/json
```
 
 
### Param (Request body) raw :
 ```
   {
    	"currency": "USD",
 		"tokens": [
           {
               "contract": "0x1a0f2ab46ec630f9fd638029027b552afa64b94c",
               "symbol": "PIE"
           }
   		]
   }
 ```
 
### SuccessExample {json} Sucess-Response:
    HtTPS 200 OK


 ```
   {
    "status": true,
    "docs": [
        {
            "id": "aston",
            "name": "Aston",
            "symbol": "PIE",
            "price": "0.0389537632",
            "percent_change_24h": "7.3",
            "contract": "0x1a0f2ab46ec630f9fd638029027b552afa64b94c",
            "image": "https://raw.githubusercontent.com/TrustWallet/tokens/master/images/0x1a0f2ab46ec630f9fd638029027b552afa64b94c.png"
        }
    ]
}
 ```
## Get Tokens List ERC20
 * @api {get} /tokens/list
 * @apiVersion 0.1.0
 * @apiName GetTokensList
 * @apiGroup Tokens
 * @apiPermission none
 * * @apiParam {String} query Query to match condition
 * @apiParam {String} networks Comma delimited list of coin index [https://github.com/satoshilabs/slips/blob/master/slip-0044.md](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) 
 * @apiParam {Boolean=true,false} [verified=true] Return only verified (meaning listed on https://coinmarketcap.com/) ERC20 contracts. If specified `false` will return both verified and not verified contracts.
 *

### Request:
```
GET : http://45.117.82.104:8003/tokens/list?query=TRX&networks=60
```



### SuccessExample {json} Sucess-Response:
    HtTPS 200 OK


 ```
{
    "docs": [
        {
            "verified": true,
            "enabled": true,
            "_id": "5aa590051125720640037236",
            "address": "0xf230b790e05390fc8295f4d3f60332c93bed42e2",
            "symbol": "TRX",
            "decimals": 6,
            "totalSupply": "100000000000000000",
            "name": "Tronix",
            "coin": 60,
            "type": "ERC20"
        }
    ]
}
 ```
 
## Get Tickers

 * @api {get} /tickers
 *
 * @apiVersion 0.1.0
 * @apiName GetTickers
 * @apiGroup Market
 * @apiPermission none
 *
 * @apiParam {String="AUD", "BRL", "CAD", "CHF", "CLP", "CNY", "CZK", "DKK", "EUR", "GBP", "HKD", "HUF", "IDR", "ILS", "INR", "JPY", "KRW", "MXN", "MYR", "NOK", "NZD", "PHP", "PKR", "PLN", "RUB", "SEK", "SGD", "THB", "TRY", "TWD", "ZAR", "USD"} [currency=USD] Coin value in curreny
 * @apiParam {String} [ids] ids Comma separated list of coin id's exp: ids=1,3,5. If ids present page_number or/and page_size will not take affect
 * @apiParam {Number} [page_number=1] Return resutls starting from specified rank
 * @apiParam {Number} [page_size=50] Return a maximum results
 * @apiParam {String} [sort=rank_asc] TODO other sort criterias: price_asc, price_desc, market_cap_asc, market_cap_desc, rank_asc, volume_24h_asc, volume_24h_desc


### Request

```
GET : http://45.117.82.104:8003/tickers?currency=EUR&page_number=1&page_size=3
```
 
### SuccessExample {json} Sucess-Response:
 
```
{
    "status": true,
    "currency": "EUR",
    "docs": [
        {
            "website_slug": "bitcoin",
            "last_updated": 1534673141,
            "percent_change_7d": 0.92,
            "percent_change_24h": -1.97,
            "percent_change_1h": -0.08,
            "market_cap": 110195598805,
            "volume_24h": 3483718875.67363,
            "price": 6399.82356254,
            "total_supply": 17218537,
            "circulating_supply": 17218537,
            "rank": 1,
            "symbol": "BTC",
            "name": "Bitcoin",
            "id": 1
        },
        {
            "website_slug": "ethereum",
            "last_updated": 1534673097,
            "percent_change_7d": -8.15,
            "percent_change_24h": -4.31,
            "percent_change_1h": -0.11,
            "market_cap": 30184177596,
            "volume_24h": 1562202981.57786,
            "price": 297.617245829,
            "total_supply": 101419451,
            "circulating_supply": 101419451,
            "rank": 2,
            "symbol": "ETH",
            "name": "Ethereum",
            "id": 1027
        },
        {
            "website_slug": "ripple",
            "last_updated": 1534673121,
            "percent_change_7d": 8.98,
            "percent_change_24h": -3.32,
            "percent_change_1h": 0.2,
            "market_cap": 13118015450,
            "volume_24h": 316370166.0248,
            "price": 0.3331779528,
            "total_supply": 99991874018,
            "circulating_supply": 39372399467,
            "rank": 3,
            "symbol": "XRP",
            "name": "XRP",
            "id": 52
        }
    ]
}
```


## Get Transactions
 * @api {get} /:networkId/transactions
 * @apiVersion 0.1.0
 * @apiName GetTransactions
 * @apiGroup Transactions
 * @apiPermission none
 *
 * @apiParam {Number} networkId Network id, supported networks are: ethereum, classic, poa, callisto
 *
 * @apiParam {String} address Address
 * @apiParam {Number} [startBlock=1] Block number to select transaction from
 * @apiParam {Number} [endBlock=9999999999] Block number to select transaction till
 * @apiParam {Number} [page=1] Number of page
 * @apiParam {Number{25..50}} [limit=25] Limit transactions per page
 * @apiParam {String} [contract] Select address transactions on specific contrac

### Request
```
GET : http://45.117.82.104:8003/ethereum/transactions?address=0x1a007089523cc763d8e7c8a2f33429b28cdae5d5

```
### SuccessExample {json} Sucess-Response:
```
{
    "docs": [
        {
            "operations": [
                {
                    "_id": "5b40dfa0354a554be0b394fb",
                    "transactionId": "0x6f9af585dbf527f67bb47f3779b9e4993da24c9b0c9e46ad86bf1175aea088fe-0",
                    "contract": {
                        "verified": false,
                        "enabled": true,
                        "_id": "5b364c1fc358f8001ba63113",
                        "address": "0x23ccc43365d9dd3882eab88f43d515208f832430",
                        "totalSupply": "500000000000000000000000000",
                        "decimals": 18,
                        "symbol": "MAS",
                        "name": "MidasProtocol"
                    },
                    "value": "30000000000000000000000",
                    "to": "0x6e7312d1028b70771bb9cdd9837442230a9349ca",
                    "from": "0xb28b47e0545fa9ee79a01a705c43372ad1c1bd5d",
                    "type": "token_transfer"
                }
            ],
            "contract": null,
            "_id": "0x6f9af585dbf527f67bb47f3779b9e4993da24c9b0c9e46ad86bf1175aea088fe",
            "blockNumber": 5922374,
            "timeStamp": "1530978210",
            "nonce": 725,
            "from": "0xb28b47e0545fa9ee79a01a705c43372ad1c1bd5d",
            "to": "0x23ccc43365d9dd3882eab88f43d515208f832430",
            "value": "0",
            "gas": "200000",
            "gasPrice": "120000000000",
            "gasUsed": "53716",
            "input": "0xa9059cbb0000000000000000000000006e7312d1028b70771bb9cdd9837442230a9349ca00000000000000000000000000000000000000000000065a4da25d3016c00000",
            "error": "",
            "id": "0x6f9af585dbf527f67bb47f3779b9e4993da24c9b0c9e46ad86bf1175aea088fe",
            "coin": 60
        }
     ]
     
  }

```
 
 
 
 

