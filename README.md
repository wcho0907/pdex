# pdex

[config](https://github.com/wcho0907/pdex/blob/master/README.md#config): Returns config data about system.<br/>
[markets](https://github.com/wcho0907/pdex/blob/master/README.md#markets): Returns all markets information about system.<br/>
[market](https://github.com/wcho0907/pdex/blob/master/README.md#market): Returns specific market information about system.<br/>

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
      url: "/v0/pdex/market?baseTokenAddress=0x0d0F936Ee4c93e25944694D6C121de94D9760F11&quoteTokenAddress=0xc778417E063141139Fce010982780140Aa0cD5Ab",
      dataType: "json",
      type : "GET",
      success : function(r) {
        console.log(r);
      }
    });
  ```
