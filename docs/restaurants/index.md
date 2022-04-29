# Restaurants

Get the list of restaurants to which this channel has subscribed

* **URL**

  `https://api.restaurantcollective.io/api/restaurants`

* **Method**

  `POST`
  
* **URL Params**

  `NONE`

* **URL Body**

```
{ 
    channel_access_code : '(your_user_code)',
    channel_access_api_key : '(your_api_key)',
    sort_field : '(name | number)',
    limit : '(n, max 500)',
    offset : '(n, default 0)'
}
```

* **Compulsory Parameters**

    * your_user_code (string) - as specified by RDL
    * your_api_key (string) - as specified by RDL
    * your_restaurant_number (string) - as specified by RDL


* **Optional Parameters**

  * sort_field (string) - 'name' or 'number' (default 'name', ascending)
  * limit (number) - the number records to return (max 100)
  * offset (number) - record offset to allow multiple calls (default 0)  
    

---

**Successful Responses**

**200 OK**

    Content:

```
{    
    restaurants : restaurants,
    status: 'OK',
    accessed: now,
    info : {
        "version": "V1.1beta",
        "release": "28/04/22",
        "tag": "RDL-API"
    }
}
```
Where *restaurants* is a JSON structure that contains an array of summary restaurant records, each of which has the following fields:

- **restaurant_name** *string*
- **restaurant_number** *string*
- **restaurant_address_1** *string*
- **restaurant_address_2** *string*
- **restaurant_address_3** *string*
- **restaurant_post_code** *string*
- **restaurant_region** *string*
- **restaurant_lat** *number*
- **restaurant_lng** *number*
- **restaurant_telephone** *string*
- restaurant_email *string*
- restaurant_website *string*
- **restaurant_spw_url** *string*
- **restaurant_cuisine_1** *string*
- **restaurant_last_updated** *string*



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
      channel_access_api_key : '(your_api_key)', 
      sort_field : 'number',
      limit : 10,
      offset : 0
    };

    let xhr_bkg_request = new XMLHttpRequest();
    xhr_bkg_request.open('POST',
    	'https://api.restaurantcollective.io/api/restaurants', true);
    	xhr_bkg_request.setRequestHeader('Content-Type', 'application/json;charset=UTF-8');
    	xhr_bkg_request.send(JSON.stringify(api_params));
```

* **Angular / TypeScript**

As would appear in an Angular service

```
 getRestaurantCore(user_code: string, api_key: string, restaurant_number: string) {
    return this.http.post('https://api.restaurantcollective.io/aoi/restaurants',
      { 
        channel_access_code : '(your_user_code)',
        channel_access_api_key : '(your_api_key)', 
        sort_field : 'number',
        limit : 10,
        offset : 0
  	  }
 }
```
---


### Examples of Use

These settings are required in the POST request body. If testing from Postman or a similar API test app, set the body format to `x-www-form-urlencoded`.

* **To return list of restaurants for this channel**
```
{ 
    channel_access_code : 'TT9999',
    channel_access_api_key : 'TESTAPIKEYASISSUEDBYRDLBYCHANNEL'
    sort_field : 'number',
    limit : 10,
    offset : 0
}
```
returns *restaurants*:

```
{
  0: {
    restaurant_address_1: "Hinton in the Hedges"
    restaurant_address_2: "Brackley"
    restaurant_address_3: "Northamptonshire"
    restaurant_cuisine_1: "British"
    restaurant_email: "jb@restaurantdevelopments.ltd"
    restaurant_last_updated: "2022-04-25T13:15:31.000Z"
    restaurant_lat: 52.0273
    restaurant_lng: -1.18677
    restaurant_name: "Example Restaurant"
    restaurant_number: "EN03085719"
    restaurant_post_code: "NN13 5NF"
    restaurant_region: "East Midlands"
    restaurant_spw_url: "https://spw.restaurantcollective.org.uk/85719-example-restaurant"
    restaurant_telephone: "077340389988"
    restaurant_website: "https://www.example-restaurant.com"
  }
  1: {
    restaurant_address_1: "31 Horsefair"
    restaurant_address_2: "Banbury"
    restaurant_address_3: "Oxfordshire"
    restaurant_cuisine_1: "British"
    restaurant_email: "info@restaurantcollective.org.uk"
    restaurant_last_updated: "2022-04-25T12:44:53.000Z"
    restaurant_lat: 52.0607
    restaurant_lng: -1.33956
    restaurant_name: "RC Demo Restaurant"
    restaurant_number: "EN03392596"
    restaurant_post_code: "OX16 0AE"
    restaurant_region: "South East England"
    restaurant_spw_url: "https://spw.restaurantcollective.org.uk/92596-rc-demo-restaurant"
    restaurant_telephone: "+44 7734038999"
    restaurant_website: "https://restaurantcollective.org.uk"
  }
}
```
