# pdex

[config](https://github.com/wcho0907/pdex/blob/master/README.md#config): Returns config data about system<br/>
[markets](https://github.com/wcho0907/pdex/blob/master/README.md#markets): Returns all markets information about system<br/>
[market](https://github.com/wcho0907/pdex/blob/master/README.md#market): Returns specific market information about system<br/>
[orderbook](https://github.com/wcho0907/pdex/blob/master/README.md#orderbook): Returns bids and asks orders of the market and related information<br/>
[challenge](https://github.com/wcho0907/pdex/blob/master/README.md#challenge): Returns a message for asking the signature<br/>
[verify](https://github.com/wcho0907/pdex/blob/master/README.md#verify): Returns the server validation of signature<br/>
[preporcess](https://github.com/wcho0907/pdex/blob/master/README.md#preprocess): Returns an intent of order for asking the signature<br/>
## config

  Returns config data about system.

* **URL**

  /v0/pdex/config

* **Method:**

  `GET`
  
*  **Arguments**

   **Required:**
 
   None

* **Returns**

  - chain - Ethereum networks
  - networkId - CHAIN_ID of Ethereum networks(https://github.com/ethereum/EIPs/blob/master/EIPS/eip-155.md)
  - contractAddress - exchange contract address based on the network above. (V1)
  - transferProxyAddress - transferProxy contract address based on the network above. (V1)

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
    ```
    {
      "chain": "ropsten",
      "networkId": 3,
      "contractAddress": "0x479CC461fEcd078F766eCc58533D6F69580CF3AC",
      "transferProxyAddress": "0x4E9Aad8184DE8833365fEA970Cd9149372FDF1e6"
    }
    ```
 * **Error Response:**

   * **Code:** 404 NOT FOUND <br />
     **Content:** `{ error : "User doesn't exist" }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/config",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex)

## markets 

  Returns all markets information about system.

* **URL**

  /v0/pdex/markets

* **Method:**

  `GET`
  
*  **Arguments**

   None

* **Returns**

	Array of MarketInfo Objects
	
	MarketInfo
  - __taker__:  taker address of the market
  - __baseToken__:  base token information of the market
  	- address  contract address of the token
  	- symbol 
  	- name
  	- tokenType
  	- status
  	- decimals
  	- icon
  	- logo 
  	- website 
  	- source_code 
  	- exchange_url 
  - __quoteToken__:  base token information of the market
  	- address: contract address of the token
  	- symbol 
  	- name
  	- tokenType
  	- status
  	- decimals
  	- icon
  	- logo 
  	- website 
  	- source_code 
  	- exchange_url   
  - __ordering__:  list order of the market
  - __cloudex_listing__:  if the market list in cloudEX 
  - __pair__:  pair symbol of the market
  - __feeInfo__:  fee information the market
    - rate:  rate(%) of the transaction fee
    - minimum:  minimum fee of transaction (Ether.)
  - __fee__:  fee data the market
    - rate:  rate of the transaction fee
    - minimum:  minimum fee of transaction (gas) 
  - __stats__:  market status in last 24 hours
    - price:  average price of last 24 hours
    - openPrice24h 
    - lowestPrice24h  
    - highestPrice24h  
    - amount24h:  total amount of last 24 hours
    - volume24h:  average price * total amount of last 24 hours
    - delta:  price - openPrice24h
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
  [
	 {
	   "taker": "0x48b08Bb52154377A2dDF2deE4A3363EE50F5A200",
	   "baseToken": {
		   "address": "0xfF67881f8d12F372d91Baae9752eB3631FF0eD00",
		   "symbol": "ZRX",
		   "name": "ZRX",
		   "tokenType": "ERC20",
		   "status": "active",
		   "decimals": 18,
		   "icon": null,
		   "logo": null,
		   "website": null,
		   "source_code": null,
		   "exchange_url": null
	   },
	   "quoteToken": {
		   "address": "0xc778417E063141139Fce010982780140Aa0cD5Ab",
		   "symbol": "WETH",
		   "name": "WETH",
		   "tokenType": "ERC20",
		   "status": "active",
		   "decimals": 18,
		   "icon": null,
		   "logo": null,
		   "website": null,
		   "source_code": null,
		   "exchange_url": null
	    },
	    "ordering": 2,
	    "cloudex_listing": "yes",
	    "pair": "ZRX/WETH",
	    "feeInfo": {
		    "rate": "0.1%",
		    "minimum": "0.003380000000000000"
		},
		"fee": {
			"rate": 0.001,
			"minimum": 650000000000000
		},
		"stats": {
			"price": "0.002796900000000000",
			"openPrice24h": "0.002802200000000000",
			"lowestPrice24h": "0.002751500000000000",
			"highestPrice24h": "0.002840900000000000",
			"amount24h": "1053.321000000000000000",
			"volume24h": "2.938798365530000000",
			"delta": "-0.000005300000000000"
		}
	 },
	...
  ]
  ```
 * **Error Response:**

   * **Code:** 404 NOT FOUND <br />
     **Content:** `{ error : "User doesn't exist" }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/markets",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex)

## market

  Returns specific market information about system.

* **URL**

  /v0/pdex/market

* **Method:**

  `GET`
  
*  **Arguments**

   - __baseTokenAddress__: contract address of base token
   - __quoteTokenAddress__: contract address of quote token

* **Returns**

	MarketInfo Object
	
	MarketInfo
  - __taker__:  taker address of the market
  - __baseToken__:  base token information of the market
  	- address  contract address of the token
  	- symbol 
  	- name
  	- tokenType
  	- status
  	- decimals
  	- icon
  	- logo 
  	- website 
  	- source_code 
  	- exchange_url 
  - __quoteToken__:  base token information of the market
  	- address: contract address of the token
  	- symbol 
  	- name
  	- tokenType
  	- status
  	- decimals
  	- icon
  	- logo 
  	- website 
  	- source_code 
  	- exchange_url   
  - __ordering__:  list order of the market
  - __cloudex_listing__:  if the market list in cloudEX 
  - __pair__:  pair symbol of the market
  - __feeInfo__:  fee information the market
    - rate:  rate(%) of the transaction fee
    - minimum:  minimum fee of transaction (Ether.)
  - __fee__:  fee data the market
    - rate:  rate of the transaction fee
    - minimum:  minimum fee of transaction (gas) 
  - __stats__:  market status in last 24 hours
    - price:  average price of last 24 hours
    - openPrice24h 
    - lowestPrice24h  
    - highestPrice24h  
    - amount24h:  total amount of last 24 hours
    - volume24h:  average price * total amount of last 24 hours
    - delta:  price - openPrice24h
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
	 {
	   "taker": "0x48b08Bb52154377A2dDF2deE4A3363EE50F5A200",
	   "baseToken": {
		   "address": "0xfF67881f8d12F372d91Baae9752eB3631FF0eD00",
		   "symbol": "ZRX",
		   "name": "ZRX",
		   "tokenType": "ERC20",
		   "status": "active",
		   "decimals": 18,
		   "icon": null,
		   "logo": null,
		   "website": null,
		   "source_code": null,
		   "exchange_url": null
	   },
	   "quoteToken": {
		   "address": "0xc778417E063141139Fce010982780140Aa0cD5Ab",
		   "symbol": "WETH",
		   "name": "WETH",
		   "tokenType": "ERC20",
		   "status": "active",
		   "decimals": 18,
		   "icon": null,
		   "logo": null,
		   "website": null,
		   "source_code": null,
		   "exchange_url": null
	    },
	    "ordering": 2,
	    "cloudex_listing": "yes",
	    "pair": "ZRX/WETH",
	    "feeInfo": {
		    "rate": "0.1%",
		    "minimum": "0.003380000000000000"
		},
		"fee": {
			"rate": 0.001,
			"minimum": 650000000000000
		},
		"stats": {
			"price": "0.002796900000000000",
			"openPrice24h": "0.002802200000000000",
			"lowestPrice24h": "0.002751500000000000",
			"highestPrice24h": "0.002840900000000000",
			"amount24h": "1053.321000000000000000",
			"volume24h": "2.938798365530000000",
			"delta": "-0.000005300000000000"
		}
	 }
  ```
 * **Error Response:**

   * **Code:** 404 NOT FOUND <br />
     **Content:** `{ error : "User doesn't exist" }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/market?baseTokenAddress=0x0d0F936Ee4c93e25944694D6C121de94D9760F11&quoteTokenAddress=0xc778417E063141139Fce010982780140Aa0cD5Ab",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex)

## orderbook

  Returns bids and asks orders of the market and related information

* **URL**

  /v0/pdex/orderbook

* **Method:**

  `GET`
  
*  **Arguments**

   - __baseTokenAddress__: contract address of base token
   - __quoteTokenAddress__: contract address of quote token

* **Returns**

	Array of bid orderInfo objects(20), array of ask orderInfo objects(20) and related information
	
	OrderInfo  bids(20), asks(20)
  - __makerTokenAddress__:  contract address of the bid/ask token
  - __takerTokenAddress__:  contract address of the pay token
  - __makerTokenAmount__:  amount of the bid token
  - __takerTokenAmount__: amount of the spend token
  - __expirationUnixTimestampSec__:  expire time of the order
  - __order_hash__
  - __intent__: order type
  - __price__: price of the order 
  - __amount__: amount of order (current)
  - __volume__: price * amount
  - __intentMakerTokenAmount__: origin amount of the bid/ask token
  - __intentTakerTokenAmount__: origin amount of the spend token
  - __remainingTakerTokenAmount__: remaining amount of the spend token
  - __makerTokenName__: name of the bid/ask token
  - __takerTokenName__: name of the spend token

  Related information
  - __spread__: value of spread
  - __maxBidPrice__: current maximum price of bid order
  - __minAskPrice__: current minimum price of ask order
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
	{
	  "bids": [
	    {
	      "makerTokenAddress": "0xc778417E063141139Fce010982780140Aa0cD5Ab",
	      "takerTokenAddress": "0x0d0F936Ee4c93e25944694D6C121de94D9760F11",
	      "makerTokenAmount": "12246548900000000",
	      "takerTokenAmount": "103270000000000000000",
	      "expirationUnixTimestampSec": "1540287123040",
	      "order_hash": "b853c002e257842678a7033f750f39bc19254ef5f3071212f05758710d88f199",
	      "intent": "buy",
	      "price": "0.000116070000000000",
	      "amount": "71.379000000000000000",
	      "volume": "0.008284960530000000",
	      "intentMakerTokenAmount": "11986548900000000",
	      "intentTakerTokenAmount": "103270000000000000000",
	      "remainingTakerTokenAmount": "71379000000000000000",
	      "makerTokenName": "WETH",
	      "takerTokenName": "MTT"
	    },
	    ...
	  ],
	  "asks": [...],
	  "spread": "0.0000045700",
	  "maxBidPrice": "0.000116070000000000",
	  "minAskPrice": "0.000120640000000000"
	}
  ```
 * **Error Response:**

   * **Code:** 404 NOT FOUND <br />
     **Content:** `{ error : "User doesn't exist" }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/orderbook?baseTokenAddress=0x0d0F936Ee4c93e25944694D6C121de94D9760F11&quoteTokenAddress=0xc778417E063141139Fce010982780140Aa0cD5Ab",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex)
## challenge

  Returns a message for asking the signature

* **URL**

  /v0/pdex/challenge

* **Method:**

  `POST`
  
*  **Arguments**

   - __address__: public address of signer

* **Returns**

	A message for taking as a input to sign for signature and payload for succeeding request
	
  - __challenge__:  hex string of message

  payload information
  - __address__: public address of signer
  - __ts__: timestamp
  - __nonce__: nonce
  - __ecSignature__: empty ecSign field for later use
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
	{
	 "challenge": "54f1e7b634eb52f0e394e2c182ef098ea46e57d0870d257af2ed981c3b59ce34",
	 "payload": 
		 {
			 "address": "0xB0EdCfBC1aB375E056E3d53fB1367f88fdb327d4", 
			 "ts": 1540288100, 
			 "nonce": "730de1d8", 
			 "ecSignature": {"v": null, "r": null, "s": null}
		 }
	}
  ```
 * **Error Response:**

   * **Code:** 404 NOT FOUND <br />
     **Content:** `{ error : "User doesn't exist" }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/challenge",
      dataType: "json",
      type : "POST",
      data:  {address:  '0xB0EdCfBC1aB375E056E3d53fB1367f88fdb327d4'},
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex) 
## verify

  Returns the server validation of signature

* **URL**

  /v0/pdex/verify

* **Method:**

  `POST`
  
*  **Arguments**
	  payload (from return of challenge)
	  - __address__: public address of signer
	  - __ts__: timestamp
	  - __nonce__: nonce
	  - __ecSignature__: returns of signed information (v, r, s)

* **Returns**

	A token for authorization and its expire time
	
  - __token__:  hex string of message
  - __expire__:  hex string of message

  payload information

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
	{"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjY3LCJpYXQiOjE1NDAzNTIzOTAsImV4cCI6MTU0MDM1Nzc5MH0.5llRMUvZyacPrRNBjjkuDclHVFoEYM9ZItSeRW7xJZo", 
	"expire": 1540357790}
  ```
 * **Error Response:**

   * **Code:** 404 NOT FOUND <br />
     **Content:** `{ error : "User doesn't exist" }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/verify",
      dataType: "json",
      type : "POST",
      data: {
      "address":"0x783a242Da80a6142f6B48BdBD4C1b9C6E1E0042F",
      "ts":1540352387,
      "nonce":"f2253e49",
      "ecSignature":
	      {
	      "v":28,
	      "r":"0x46b4ffd3b940ebeb5889ab27b0a2a02858ef31904290a696692361d3a1ac91a9",
	      "s":"0x785672547b5ccd1260d5ccf93a47f6a486f167a347ac3e775c249dc2b1c9b783"
	      }
	  },
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex) 
## preprocess

  Returns an intent of order for asking the signature

* **URL**

  /v0/pdex/preprocess

* **Method:**

  `POST`
  
*  **Arguments**
	  request of order intent
	  - __maker__: public address of signer
	  - __baseTokenAddress__: address of base token 
	  - __quoteTokenAddress__: address of quote token 
	  - __intent__: order type (buy/sell)
	  - __amount__:  amount of order
	  - __price__: price of order

* **Returns**

	order intent information for signing
	
  - __intent__
	  - base: symbol of  base token
	  - baseTokenAddress: address of base token
	  - quote: symbol of quote token
	  - quoteTokenAddress: address of quote token
	  - amount: amount of order
	  - volume: price * amount
	  - price: price of order
	  - intent: order type (buy/sell)
	  - feeRate: rate of fee
	  - feeMinimum: minimum fee
	  - makerTokenAmount: amount of the maker token
	  - takerTokenAmount: amount of the taker token
	  - checksum
  - __order__
	  - exchangeContractAddress: contract address of exchange
	  - maker: address of maker
	  - taker: address of taker
	  - feeRecipient: recipient of fee
	  - makerFee: fee of maker
	  - takerFee: fee  of taker
	  - makerTokenAddress: address of maker token
	  - takerTokenAddress: address of taker token
	  - makerTokenAmount: amount of maker token
	  - takerTokenAmount: amount of taker token
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
	{
		"order": {
			"exchangeContractAddress": "0x479CC461fEcd078F766eCc58533D6F69580CF3AC", 
			"maker": "0x783a242Da80a6142f6B48BdBD4C1b9C6E1E0042F", 
			"taker": "0x4Bda106325C335dF99eab7fE363cAC8A0ba2a24D", 
			"feeRecipient": "0x0000000000000000000000000000000000000000", 
			"makerFee": "0", 
			"takerFee": "0", 
			"makerTokenAddress": "0xc778417E063141139Fce010982780140Aa0cD5Ab", 
			"takerTokenAddress": "0x0d0F936Ee4c93e25944694D6C121de94D9760F11", 
			"makerTokenAmount": "12890000000000000", 
			"takerTokenAmount": "100000000000000000000"
		}, 
		"intent": {
			"base": "MTT", 
			"baseTokenAddress": "0x0d0F936Ee4c93e25944694D6C121de94D9760F11", 
			"quote": "WETH", 
			"quoteTokenAddress": "0xc778417E063141139Fce010982780140Aa0cD5Ab", 
			"amount": "100", 
			"volume": "0.0125000", 
			"price": "0.0001250", 
			"intent": "buy", 
			"feeRate": "0.001", 
			"feeMinimum": "390000000000000", 
			"makerTokenAmount": "12500000000000000", 
			"takerTokenAmount": "100000000000000000000", 
			"checksum": "ab5f0276b1:f8d929d5a3daeadd69abca747987ee06"
		}
	}
  ```
 * **Error Response:**

   * **Code:** 400 Bad Request <br />
    **subcode, reason ** 
101,  'Malformed JSON' <br/>
102, 'Invalid token address'<br/>
103, 'Unsupported trading pair'<br/>
104, 'Invalid intent'<br/>
106,  'Invalid price'<br/>
107,  'Invalid precision for price'<br/>
108,  'Invalid amount'<br/>
109,  'Invalid precision for amount'<br/>
105,  'Price or amount not provided'<br/>
111, 'Allowance not enabled for quote-token'<br/>
112,  'Insufficient of balance for quote-token'<br/>
113,  'Allowance not enabled for base-token'<br/>
114,  'Insufficient of balance for base-token'<br/>
110,  ' amount (%d<%d)'  % (volume_deno, min_fee*2)'<br/>


* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/preprocess",
      dataType: "json",
      type : "POST",
      data:
		{
			"maker":"0x783a242Da80a6142f6B48BdBD4C1b9C6E1E0042F",
			"baseTokenAddress":"0x0d0F936Ee4c93e25944694D6C121de94D9760F11",
			"quoteTokenAddress":"0xc778417E063141139Fce010982780140Aa0cD5Ab",
			"intent":"buy",
			"amount":"100",
			"price":"0.0001250"
		}
	  ,
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex) 
