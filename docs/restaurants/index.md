# Restaurants

Returns a list of restaurants to which this channel has subscribed

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
    limit : '(n, max 100)',
    offset : '(n, default 0)'
}
```

* **Compulsory Parameters**

    * your_user_code (string) - as specified by RDL
    * your_api_key (string) - as specified by RDL


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
Where *restaurants* is a JSON structure that contains an array of summary restaurant records, each of which has the following fields (those in bold will always be returned):

- **name** *string*
- **number** *string*
- **address_1** *string*
- **address_2** *string*
- **address_3** *string*
- **post_code** *string*
- **region** *string*
- **lat** *number*
- **lng** *number*
- **telephone** *string*
- email *string*
- website *string*
- spw_url *string*
- **cuisine_1** *string*
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
Error texts can also be `'No restaurants authorised for this api user'`, 
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
 getRestaurants(user_code, api_key, sort_field, limit, offset) {
    return this.http.post('https://api.restaurantcollective.io/aoi/restaurants',
      { 
        channel_access_code : '(your_user_code)',
        channel_access_api_key : '(your_api_key)', 
        sort_field, limit, offset
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
returns (count is the number of restaurants returned, offset is the index of the first record, total is the total number of restaurants available for this channel. This example is equivalent to 'returning records 1 to 2 of 2'):

```
{
  count: 2,
  offset: 0,
  total: 2,
  restaurants: {
    0: {
      address_1: "Hinton in the Hedges"
      address_2: "Brackley"
      address_3: "Northamptonshire"
      cuisine_1: "British"
      email: "jb@restaurantdevelopments.ltd"
      last_updated: "2022-04-25T13:15:31.000Z"
      lat: 52.0273
      lng: -1.18677
      name: "Example Restaurant"
      number: "EN03085719"
      post_code: "NN13 5NF"
      region: "East Midlands"
      spw_url: "https://spw.restaurantcollective.org.uk/85719-example-restaurant"
      telephone: "077340389988"
      website: "https://www.example-restaurant.com"
    }
    1: {
      address_1: "31 Horsefair"
      address_2: "Banbury"
      address_3: "Oxfordshire"
      cuisine_1: "British"
      email: "info@restaurantcollective.org.uk"
      last_updated: "2022-04-25T12:44:53.000Z"
      lat: 52.0607
      lng: -1.33956
      name: "RC Demo Restaurant"
      number: "EN03392596"
      post_code: "OX16 0AE"
      region: "South East England"
      spw_url: "https://spw.restaurantcollective.org.uk/92596-rc-demo-restaurant"
      telephone: "+44 7734038999"
      website: "https://restaurantcollective.org.uk"
    }
  }
}
```
