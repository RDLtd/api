# Restaurant Core

Returns the core data set for a restaurant

* **URL**

  `https://api.restaurantcollective.io/api/restaurant_core`

* **Method**

  `POST`
  
* **URL Params**

  `NONE`

* **URL Body**

```
{ 
    user_code : '(your_user_code)',
    api_key : '(your_api_key)',
    restaurant_number : '(specific restaurant number)'
}
```

* **Compulsory Parameters**

    * your_user_code (string) - as specified by RDL
    * your_api_key (string) - as specified by RDL
    * your_restaurant_number (string) - as specified by RDL
    
    

---

**Successful Responses**

**200 OK**

    Content:

```
{    
    restaurant_core : restaurant_core,
    status: 'OK',
    accessed: now,
    info : {
        "version": "V1.1beta",
        "release": "28/04/22",
        "tag": "RDL-API"
    }
}
```
Where *restaurant_core* is a JSON structure that contains all currently available *core data* for a restaurant
(values in bold should always be returned):

- **number** *string*
- group_name *string*
- **name** *string*
- **address_1** *string*
- **address_2** *string*
- **address_3** *string*
- **post_code** *string*
- **region** *string*
- **country_code** *string*
- **lat** *number*
- **lng** *number*
- **telephone** *string*
- email *string*
- website *string*
- **spw_url** *string*
- **spw_type** *string* [ member / curated / stock ]
- facebook *string*
- twitter *string*
- instagram *string*
- **cuisine_1** *string*
- cuisine_2 *string*
- **last_updated** *string*



**Error Responses**

**400 BAD REQUEST**

    Content:

```
{
    error : 'Invalid Restaurant Number',
    status : 'FAIL',
    accessed : (datetime),
    api_version : {
        version : 'V1.0beta',
        release : '28/04/22',
        tag : 'RDL_API'
    }
}
```

**403 UNAUTHORISED**

    Content:

```
{
    error : 'Failed to verify user',
    status : 'FORBIDDEN',
    accessed : (datetime),
    api_version : {
        "version": "V1.1beta",
        "release": "28/04/22",
        "tag": "RDL-API"
    }
}
```
Error texts can also be `'No restaurants authorised for this api user'`, `'Restaurant (number) is not authorised for this api user'`,
`'Unable to determine if restaurant is authorised'`, `'Failed to read api users database'`. In all cases if these cannot be resolved, please contact our technical support team.



**404 DATABASE ERROR**

    Content:

```
{
    error : '(message)',
    status : 'FAIL',
    accessed : (datetime),
    api_version : {
        "version": "V1.1beta",
        "release": "28/04/22",
        "tag": "RDL-API"
    }
}
```
---


### Implementation



* **HTML / JavaScript**

As would appear in a script
```
    let api_params = {
      user_code : '(your_user_code)',
      api_key : '(your_api_key)', 
      restaurant_number : 'EN044999999'
    };

    let xhr_bkg_request = new XMLHttpRequest();
    xhr_bkg_request.open('POST',
      'https://api.restaurantcollective.io/api/restaurant_core', true);
      xhr_bkg_request.setRequestHeader('Content-Type', 'application/json;charset=UTF-8');
      xhr_bkg_request.send(JSON.stringify(api_params));
```

* **Angular / TypeScript**

As would appear in an Angular service

```
 getRestaurantCore(user_code, api_key, restaurant_number) {
    return this.http.post('https://api.restaurantcollective.io/api/restaurant_core',
      { 
        user_code : '(your_user_code)',
        api_key : '(your_api_key)', 
        restaurant_number
      }
 }
```
---


### Examples of Use

These settings are required in the POST request body. If testing from Postman or a similar API test app, set the body format to `x-www-form-urlencoded`.

* **To return detail content for one restaurant**
```
{ 
    user_code : 'TT9999',
    api_key : 'TESTAPIKEYASISSUEDBYRDLBYCHANNEL'
    restaurant_number : 'EN044999999'
}
```
returns *restaurant_core*:

```
{
  number: "EN03392596",
  group_name: "RDL",
  name: "RC Demo Restaurant",
  
  address_1: "Kineton House, 31 Horsefair",
  address_2: "Banbury",
  address_3: "Oxfordshire",
  post_code: "OX16 0AE",
  country_code: "GB",
  lat: 52.0607,
  lng: 1.33956,

  telephone: "+44 7734038999",
  email: "info@restaurantcollective.org.uk",
  website: "https://restaurantcollective.org.uk",
  spw_url: "https://spw.restaurantcollective.org.uk/92596-rc-demo-restaurant/",
  spw_type: "member",
  
  facebook: "https://faceboook.com/restaurantcollective",
  twitter: "https://twitter.com/RCollectiveUK",
  instagram: "https://instagram.com/restaurantcollectiveuk",
  
  cuisine_1: "British",
  cuisine_2: "Cafe",
  
  last_updated: "2019-06-13T09:45:14.000Z",
}
```
