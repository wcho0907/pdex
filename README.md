# pdex

[config](#config): Returns config data about system<br/>
[markets](#markets): Returns all markets information about system<br/>
[market](#market): Returns specific market information about system<br/>
[orderbook](#orderbook): Returns bids and asks orders of the market and related information<br/>
[challenge](#challenge): Returns a message for asking the signature<br/>
[verify](#verify): Returns the server validation of signature<br/>
[preporcess](#preprocess): Returns an intent of order for asking the signature<br/>
[submit](#submit): Returns the validation of order signature<br/>
[order](#order): Returns order information by specific order_hash<br/>
[myorders](#myorders): Returns orders information of logged in user with conditions<br/>
[cancel-order](#cancel-order): Cancel order by specific order_hash<br/>
[trade-history](#trade-history): Returns trade history data (price, amount, time) of system</br>
[wallet/locked](#walletlocked): Returns total unsettled volume of quote token(buy order) or base token(sell order)<br/>
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
	
  - __token__
  - __expire__:  expired time of token
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
    **subcode, reason** <br />
```    
	101,  'Malformed JSON' 
	102,  'Invalid token address'
	103,  'Unsupported trading pair'
	104,  'Invalid intent'
	106,  'Invalid price'
	107,  'Invalid precision for price'
	108,  'Invalid amount'
	109,  'Invalid precision for amount'
	105,  'Price or amount not provided'
	111,  'Allowance not enabled for quote-token'
	112,  'Insufficient of balance for quote-token'
	113,  'Allowance not enabled for base-token'
	114,  'Insufficient of balance for base-token'
	110,  'amount (%d<%d)'  % (volume_deno, min_fee*2)'
```

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
## submit

  Returns the validation of order signature

* **URL**

  /v0/pdex/submit

* **Method:**

  `POST`
  
*  **Arguments**
	  order intent information with signature
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
		  - expirationUnixTimestampSec: expired time of order
		  - salt: salt of the ecSignature
		  - ecSignature: - returns of signed information (v, r, s)
* **Returns**
			validation information
			
  - order_hash
  - token
  - expire: expired time of token
	

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
		{
			"order_hash": "9045d49eb0112ac6b860cfc25e5146cbf199696444ee6d344e523ec20564fba1",
			"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjY3LCJpYXQiOjE1NDAzNjYwMTgsImV4cCI6MTU0MDM3MTQxOH0.hmtULkVH6JyCpn1Vk_l8v_l_18KEs8RU3QxrQkVZbf8", 
			"expire": 1540371418
		 }
  ```
 * **Error Response:**

   * **Code:** 400 Bad Request <br />
		  
* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/submit",
      dataType: "json",
      type : "POST",
      data:
		{
			"order":{
				"exchangeContractAddress":"0x479cc461fecd078f766ecc58533d6f69580cf3ac",
				"maker":"0x783a242da80a6142f6b48bdbd4c1b9c6e1e0042f",
				"taker":"0x54e0bfe2f148edaba0570bb1bf52a93fae478c9f",
				"makerTokenAddress":"0xc778417e063141139fce010982780140aa0cd5ab",
				"takerTokenAddress":"0x2e11c118123e36c44e3d964bf0405552eea04605",
				"feeRecipient":"0x0000000000000000000000000000000000000000",
				"makerTokenAmount":"427213440000000000",
				"takerTokenAmount":"123000000000000000000",
				"makerFee":"0",
				"takerFee":"0",
				"expirationUnixTimestampSec":"1540452413472",
				"salt":"22613246247772084676703019028017946719169894782291294370367974348516328675199",
				"ecSignature":{
					"v":27,
					"r":"0xa77840b483744efb0d08b7e69e4b1c2b8904b2437d3ff72bb75b12eaa3161764",
					"s":"0x4633b3ca09c306a9670169fcaafc03ef6da279be7e2ee9358a84b21ae451bdd7"
				}
			},
			"intent":{
				"base":"TEST1",
				"baseTokenAddress":"0x2e11C118123e36C44e3D964Bf0405552eea04605",
				"quote":"WETH",
				"quoteTokenAddress":"0xc778417E063141139Fce010982780140Aa0cD5Ab",
				"amount":"123",
				"volume":"0.425088",
				"price":"0.003456",
				"intent":"buy",
				"feeRate":"0.005",
				"feeMinimum":"390000000000000",
				"makerTokenAmount":"425088000000000000",
				"takerTokenAmount":"123000000000000000000",
				"checksum":"9e6023eb3e:cffc0cb2ee9916eecd61fbe64a1aae94"
				}
			}
		}
	  ,
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex) 
## order

  Returns order information by specific order_hash

* **URL**

  /v0/pdex/order

* **Method:**

  `GET`
  
*  **Arguments**
	  - __order_hash__
	 
* **Returns**
			order(intent|array of filled|array of pending) information
  - __order__
	  - maker: address of maker
	  - makerTokenAddress: contract address of maker token
	  - makerTokenAmount: amount of maker
	  - takerTokenAddress: contract address of taker token
	  - takerTokenAmount: amount of taker
	  - expirationUnixTimestampSec: expired time of order
	  - takerTokenAmountLocked: locked amount of taker token
	  - takerTokenAmountFilled: filled amount of taker token
	  - takerTokenAmountCancelled: cancelled amount of taker token
	  - order_hash
	  - time_submitted
	  - status: new/open/closed/expired/cancelled
	  - refundStatus: not-available/claimable/claimed/refunded/pending
	  - avgPrice
	  - filledAmount
	  - volume
	  - paid
	  - fee
	  - refund
  - __intent__
	  - baseTokenName: symbol of the base token
	  - quoteTokenName: symbol of the quote token
	  - intent: order intent - (buy/sell)
	  - price
	  - amount
	  - volume
	  - feeRate
	  - feeMinimum
  - __filled[]__
	  - id:
	  - orderId: sequence number of order
	  - baseTokenAddress
	  - quoteTokenAddress
	  - intent
	  - price
	  - amount
	  - volume
	  - matchId: sequence number of match
	  - txHash: hash of the transaction in chain
	  - blockNumber: block of the transaction happened
	  - gasUsed: used gas
	  - filledMakerTokenAmount
	  - filledTakerTokenAmount
	  - paid
	  - fee
	  - refund
	  - time_filled
  - __pending[]__
	  - matchId
	  - price
	  - amount
	  - txHash
	  - time_matched
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
	{
	"order":
		{
			"maker":"0x21B93E9B4De782787993eE4d3289c45A3024c862",
			"makerTokenAddress":"0xfF67881f8d12F372d91Baae9752eB3631FF0eD00",
			"makerTokenAmount":"100000000000000000000",
			"takerTokenAddress":"0xc778417E063141139Fce010982780140Aa0cD5Ab",
			"takerTokenAmount":"279720000000000000",
			"expirationUnixTimestampSec":"1540460471044",
			"takerTokenAmountLocked":"27972000000000000",
			"takerTokenAmountFilled":"195804000000000000",
			"takerTokenAmountCancelled":"0",
		    "order_hash":
		"27815f2d6d271fafb5ca4f248feb6a61e54c9e6a053b9990304f0c7b16283264",
			"time_submitted":"2018-10-24T09:41:14.365000Z",
			"status":"open",
			"refundStatus":"not-available",
			"avgPrice":"0.002800000000000000",
			"filledAmount":"70.000000000000000000",
			"volume":"0.196000000000000000",
			"paid":"0.195804000000000000",
			"fee":"0.000196000000000000",
			"refund":"0.000000000000000000"
		},
	"intent":
		{
			"baseTokenName":"ZRX",
			"quoteTokenName":"WETH",
			"intent":"sell",
			"price":"0.002800000000000000",
			"amount":"100.000000000000000000",
			"volume":"0.280000000000000000",
			"feeRate":"0.00100",
			"feeMinimum":"0.000130000000000000"
		},
	"filled":
		[
			{
				"id":6197,
				"orderId":13503,
				"baseTokenAddress":"0xfF67881f8d12F372d91Baae9752eB3631FF0eD00",
				"quoteTokenAddress":"0xc778417E063141139Fce010982780140Aa0cD5Ab",
				"intent":"sell",
				"price":"0.002800000000000000",
				"amount":"50.000000000000000000",
				"volume":"0.140000000000000000",
				"matchId":6438,
				"txHash":"0xd5902bea40514c7e5501664b9b6933404fff24edfadbfdb9c810157aaf07a8c7",
				"blockNumber":4291516,
				"gasUsed":"0.000201942",
				"filledMakerTokenAmount":"50000000000000000000",
				"filledTakerTokenAmount":"139860000000000000",
				"paid":"0.139860000000000000",
				"fee":"0.000140000000000000",
				"refund":"0.000000000000000000",
				"time_filled":"2018-10-24T09:44:34Z"
			}
		],
	"pending":
		[
			{
				"matchId":6440,
				"price":0.0028,
				"amount":"10.000000000000000000",
				"txHash":"0xbdcfa00c9d0903eabf0ea1eaa732aeb9969725203bac983dd2d02f3e98b49991",
				"time_matched":"2018-10-24T09:51:21Z"
			}
		]
	}   
  ```
 * **Error Response:**

   * **Code:** 400 Bad Request <br />
		  
* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/order?order_hash=27815f2d6d271fafb5ca4f248feb6a61e54c9e6a053b9990304f0c7b16283264",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex) 
## myorders

  Returns orders information of logged in user with conditions

* **URL**

  /v0/pdex/myorders

* **Method:**

  `GET`
*  **Headers**  
	- __authorization__: 'Bearer ' + token string of logged in user 

*  **Arguments**
	  - __filter__: all/open/history
	  - __offset__: starting position
	  - __limit__: specified number
	 
* **Returns**
			Array of logged in user's order(s) and wallet locked information
			
  - __order[]__
	  - __order__
		  - maker: address of maker
		  - makerTokenAddress: contract address of maker token
		  - makerTokenAmount: amount of maker
		  - takerTokenAddress: contract address of taker token
		  - takerTokenAmount: amount of taker
		  - expirationUnixTimestampSec: expired time of order
		  - takerTokenAmountLocked: locked amount of taker token
		  - takerTokenAmountFilled: filled amount of taker token
		  - takerTokenAmountCancelled: cancelled amount of taker token
		  - order_hash
		  - time_submitted
		  - status: new/open/closed/expired/cancelled
		  - refundStatus: not-available/claimable/claimed/refunded/pending
		  - avgPrice
		  - filledAmount
		  - volume
		  - paid
		  - fee
		  - refund
	  - __intent__
		  - baseTokenName: symbol of the base token
		  - quoteTokenName: symbol of the quote token
		  - intent: order intent - (buy/sell)
		  - price
		  - amount
		  - volume
		  - feeRate
		  - feeMinimum
	  - __filled[]__
		  - id:
		  - orderId: sequence number of order
		  - baseTokenAddress
		  - quoteTokenAddress
		  - intent
		  - price
		  - amount
		  - volume
		  - matchId: sequence number of match
		  - txHash: hash of the transaction in chain
		  - blockNumber: block of the transaction happened
		  - gasUsed: used gas
		  - filledMakerTokenAmount
		  - filledTakerTokenAmount
		  - paid
		  - fee
		  - refund
		  - time_filled
	  - __pending[]__
		  - matchId
		  - price
		  - amount
		  - txHash
		  - time_matched
  - __walletLocked__
	  - [contract address of token]: total unsettled volume of quote token(buy order) or base token(sell order)
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
	{"orders": 
	[   
		{
		"order":
			{
				"maker":"0x21B93E9B4De782787993eE4d3289c45A3024c862",
				"makerTokenAddress":"0xfF67881f8d12F372d91Baae9752eB3631FF0eD00",
				"makerTokenAmount":"100000000000000000000",
				"takerTokenAddress":"0xc778417E063141139Fce010982780140Aa0cD5Ab",
				"takerTokenAmount":"279720000000000000",
				"expirationUnixTimestampSec":"1540460471044",
				"takerTokenAmountLocked":"27972000000000000",
				"takerTokenAmountFilled":"195804000000000000",
				"takerTokenAmountCancelled":"0",
			    "order_hash":
			"27815f2d6d271fafb5ca4f248feb6a61e54c9e6a053b9990304f0c7b16283264",
				"time_submitted":"2018-10-24T09:41:14.365000Z",
				"status":"open",
				"refundStatus":"not-available",
				"avgPrice":"0.002800000000000000",
				"filledAmount":"70.000000000000000000",
				"volume":"0.196000000000000000",
				"paid":"0.195804000000000000",
				"fee":"0.000196000000000000",
				"refund":"0.000000000000000000"
			},
		"intent":
			{
				"baseTokenName":"ZRX",
				"quoteTokenName":"WETH",
				"intent":"sell",
				"price":"0.002800000000000000",
				"amount":"100.000000000000000000",
				"volume":"0.280000000000000000",
				"feeRate":"0.00100",
				"feeMinimum":"0.000130000000000000"
			},
		"filled":
			[
				{
					"id":6197,
					"orderId":13503,
					"baseTokenAddress":"0xfF67881f8d12F372d91Baae9752eB3631FF0eD00",
					"quoteTokenAddress":"0xc778417E063141139Fce010982780140Aa0cD5Ab",
					"intent":"sell",
					"price":"0.002800000000000000",
					"amount":"50.000000000000000000",
					"volume":"0.140000000000000000",
					"matchId":6438,
					"txHash":"0xd5902bea40514c7e5501664b9b6933404fff24edfadbfdb9c810157aaf07a8c7",
					"blockNumber":4291516,
					"gasUsed":"0.000201942",
					"filledMakerTokenAmount":"50000000000000000000",
					"filledTakerTokenAmount":"139860000000000000",
					"paid":"0.139860000000000000",
					"fee":"0.000140000000000000",
					"refund":"0.000000000000000000",
					"time_filled":"2018-10-24T09:44:34Z"
				}
			],
		"pending":
			[
				{
					"matchId":6440,
					"price":0.0028,
					"amount":"10.000000000000000000",
					"txHash":"0xbdcfa00c9d0903eabf0ea1eaa732aeb9969725203bac983dd2d02f3e98b49991",
					"time_matched":"2018-10-24T09:51:21Z"
				}
			]
		} 
	],
	"filter": "open", 
	"offset": 0, 
	"total": 45, 
	"walletLocked": {"0x0d0F936Ee4c93e25944694D6C121de94D9760F11": "5483895999999000010398"} 
	} 
  ```
 * **Error Response:**

   * **Code:** 400 Bad Request <br />
		  
* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/myorders?filter=open&offset=0&limit=100",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex) 
## cancel-order

  Cancel by specific order_hash

* **URL**

  /v0/pdex/cancel-order

* **Method:**

  `GET`
*  **Arguments**
	  - __order_hash__
* **Returns**
			None
* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
   ```
	N/A
  ```
 * **Error Response:**

   * **Code:** 400 Bad Request <br />
		  
* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/cancel-order",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
  [:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex) 
## trade-history

  Returns trade history data (price, amount, time) of system.

* **URL**

  /v0/pdex/trade-history

* **Method:**

  `GET`
  
*  **Arguments**

   - __baseTokenAddress__: contract address of base token
   - __quoteTokenAddress__: contract address of quote token

* **Returns**

  - __History[]__
	  - time
	  - price
	  - amount
	  - trend: up/down
  - __count__  number of array    
  - __baseToken__: symbol of base token
  - __quoteToken__: symbol of quote token
  - __baseTokenAddress__: contract address of base token
  - __quoteTokenAddress__: contract address of quote token

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
    ```
	{"history": 
	[
		{
			"time": "2018-10-25T06:09:10Z", 
			"price": 0.002804400000000000, 
			"amount": "15.127200000000000000", 
			"trend": "down"
		}
	], 
	"count": 20, 
	"baseToken": "ZRX", 
	"quoteToken": "WETH", 
	"baseTokenAddress": "0xfF67881f8d12F372d91Baae9752eB3631FF0eD00",
	"quoteTokenAddress": "0xc778417E063141139Fce010982780140Aa0cD5Ab"}
    ```
 * **Error Response:**

   * **Code:** 404 NOT FOUND <br />
     **Content:** `{ error : "User doesn't exist" }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/trade-history?baseTokenAddress=0xfF67881f8d12F372d91Baae9752eB3631FF0eD00&quoteTokenAddress=0xc778417E063141139Fce010982780140Aa0cD5Ab",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex)
## wallet/locked

  Returns total unsettled volume of quote token(buy order) or base token(sell order)

* **URL**

  /v0/pdex/wallet/locked

* **Method:**

  `GET`
*  **Headers**  
	- __authorization__: 'Bearer ' + token string of logged in user   
*  **Arguments**
	None
* **Returns**

	- [contract address of token]: total unsettled volume of quote token(buy order) or base token(sell order)

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** 
    ```
	{"0xc778417E063141139Fce010982780140Aa0cD5Ab": "33000000000000000"}
    ```
 * **Error Response:**

   * **Code:** 404 NOT FOUND <br />
     **Content:** `{ error : "User doesn't exist" }`

* **Sample Call:**

  ```javascript
    $.ajax({
      url: "/v0/pdex/wallet/locked",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex)
