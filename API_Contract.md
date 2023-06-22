***CUSTOMERS***
----
* Customer object
```
{
  id: integer
  fullname: string
  picture: string `Base64 string`
  phone: string
  points: integer
  rewards_number: integer 
}
```
**GET /customers/:id**
----
  Returns the specified Customer.
* **URL Params**  
  *Required:* `id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: `<Auth Token>` Defined by Odoo-Tec to authorize API access
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ <customer_object> }` 
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "Customer doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`
  
**POST /Customers**
----
  Creates a new Customer and returns the new object.
* **URL Params**  
  None
* **Headers**  
  Content-Type: application/json  
* **Data Params**  
```
  {
    fullname: string
    phone: string
  }
```
* **Success Response:**  
* **Code:** 200  
  **Content:**  `{ <customer_object> }` 

**PUT /Customers/:id/info**
----
  Updates fields on the specified Customer and returns the updated object.
* **URL Params**  
  *Required:* `id=[integer]`
* **Data Params**  
```
  {
  	fullname: string
    picture: string
  }
```
* **Headers**  
  Content-Type: application/json   
  Authorization: Bearer `<OAuth Token>`
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ <customer_object> }`  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "Customer doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

**GET /customers/:id/orders**
----
  Returns all Orders associated with the specified customer.
* **URL Params**  
  *Required:* `id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: `<OAuth Token>`
* **Success Response:**  
* **Code:** 200  
  **Content:**  
```
{
  orders: [
           {<order_object>},
           {<order_object>},
           ...
         ]
}
```
* Order object
```
{
  id: integer
  customer_id: <user_id>
  total: float(2)
  items: [
              { 
                product_id: integer
                name: string
                img: string
                quantity: integer
                price: float(2)
              },
              { 
                product_id: integer
                name: string
                img: string
                quantity: integer
                price: float(2)
              },
              ...
            ]
  created_at: datetime
  updated_at: datetime
}
```  
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "Customer doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

***STORES***
#Could be POS on Odoo
----
* Store object
```
{
  id: integer
  name: string
  lat: string
  long: string 
}
```
**GET /stores**
----
  Returns the specified Customer.
* **URL Params**  
  None
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: `<Auth Token>` Defined by Odoo-Tec to authorize API access
* **Success Response:** 
* **Code:** 200  
  **Content:**  `{ <store_object> }` 
* **Error Response:**  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

**GET /stores/:id/categories**
----
  Returns this store categories.
* Category object
```
{
  id: integer
  name: string
  parent_id: integer
}
```
* **URL Params**  
  *Required:* `id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: `<Auth Token>` Defined by Odoo-Tec to authorize API access
* **Success Response:** 
* **Code:** 200  
  **Content:**  
  ```
  {
    categories: [
      { <category_object> }
    ]
  }
  ```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "Store doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

**GET /stores/:id/products**
----
  Returns store's available products considering stock availability.
* Short Product object
```
{
  id: integer
  name: string
  image: string
  price: float(2)
  category_id: integer
  quantity: integer
  updated_at: datetime --For sorting
  tag: string --Ex: Hot, New, Deal 
}
```
* **URL Params**  
  *Required:* `id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: `<Auth Token>` Defined by Odoo-Tec to authorize API access
* **Success Response:** 
* **Code:** 200  
  **Content:**  
  ```
  {
    products: [
      { <short_product_object> }
    ]
  }
  ```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "Store doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`

  **GET /stores/:id/products/:product_id**
----
  Returns store's product details considering stock availability .
* Full Product object
```
{
  id: integer
  name: string
  description: string
  image: string
  price: float(2)
  category: { 
      id: integer
      name: string
    }
  quantity: integer
  tag: string //Ex: Hot, New, Deal 
  attributes: [
    {
      id: integer
      attribute: string
      values: [
        { 
          id: integer
          value: string
          price: float(2) //if selection should accumulate to price
        }
      ]
    }
  ]
  ingredients: [
    { 
      name: string
      value: string
    }
  ]
}
```
* **URL Params**  
  *Required:* `id=[integer]`
* **Data Params**  
  None
* **Headers**  
  Content-Type: application/json  
  Authorization: `<Auth Token>` Defined by Odoo-Tec to authorize API access
* **Success Response:** 
* **Code:** 200  
  **Content:**  
  ```
  {
    products: [
      { <short_product_object> }
    ]
  }
  ```
* **Error Response:**  
  * **Code:** 404  
  **Content:** `{ error : "Store doesn't exist" }`  
  OR  
  * **Code:** 401  
  **Content:** `{ error : "You are unauthorized to make this request." }`