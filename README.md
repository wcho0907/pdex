# pdex

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

  None

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


