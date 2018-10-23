# pdex
:top:
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
---  
## markets
[:top:](https://github.com/wcho0907/pdex/blob/master/README.md#pdex)
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
