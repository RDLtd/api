# Restaurant Outline

Access the outline data set for restaurant

* **URL**

  `https://api.restaurantcollective.io/api/restaurant_outline`

* **Method**

  `POST`
  
* **URL Params**

  `NONE`

* **URL Body**

```
{ 
    channel_access_code : '(your_user_code)',
    channel_access_api_key : '(your_api_key)',
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
    restaurant_outline : restaurant_outline,
    status: 'OK',
    accessed: now,
    info : {
        "version": "V1.1beta",
        "release": "28/04/22",
        "tag": "RDL-API"
    }
}
```
Where *restaurant_outline* is a JSON structure that contains all currently available *core data* plus a subset of additional data for a restaurant (values in bold should always be returned):

- **restaurant_number** *string*
- restaurant_group_name *string*
- **restaurant_name** *string*
- **restaurant_address_1** *string*
- **restaurant_address_2** *string*
- **restaurant_address_3** *string*
- **restaurant_post_code** *string*
- **restaurant_region** *string*
- **restaurant_country_code** *string*
- **restaurant_lat** *number*
- **restaurant_lng** *number*
- **restaurant_telephone** *string*
- restaurant_email *string*
- restaurant_website *string*
- **restaurant_spw_url** *string*
- **restaurant_spw_type** *string* [ member / curated / stock ]
- restaurant_facebook *string*
- restaurant_twitter *string*
- restaurant_instagram *string*
- **restaurant_opening_hours** 
- **restaurant_cuisine_1** *string*
- restaurant_cuisine_2 *string*
- **restaurant_image_cdn:** *string*
- **restaurant_image_path:** *string*
- **restaurant_opening_hours:** *object*
- restaurant_opening_notes: *string*
- **restaurant_attributes:** *object*
- **restaurant_description** *string*
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
      restaurant_number : 'EN044999999'
    };

    let xhr_bkg_request = new XMLHttpRequest();
    xhr_bkg_request.open('POST',
    	'https://api.restaurantcollective.io/api/restaurant_outline', true);
    	xhr_bkg_request.setRequestHeader('Content-Type', 'application/json;charset=UTF-8');
    	xhr_bkg_request.send(JSON.stringify(api_params));
```

* **Angular / TypeScript**

As would appear in an Angular service

```
 getRestaurantOutline(user_code: string, api_key: string, restaurant_number: string) {
    return this.http.post('https://api.restaurantcollective.io/api/restaurant_outline',
      { 
        channel_access_code : '(your_user_code)',
        channel_access_api_key : '(your_api_key)', 
        restaurant_number: '(restaurant_number)'
  	  }
 }
```
---


### Examples of Use

These settings are required in the POST request body. If testing from Postman or a similar API test app, set the body format to `x-www-form-urlencoded`.

* **To return detail content for one restaurant**
```
{ 
    channel_access_code : 'TT9999',
    channel_access_api_key : 'TESTAPIKEYASISSUEDBYRDLBYCHANNEL'
    restaurant_number : 'EN044999999'
}
```
returns *restaurant_outline*:

```
{
  "restaurant_number": "EN03392596",
  "restaurant_group_name": "RDL",
  "restaurant_name": "RC Demo Restaurant",
  
  "restaurant_address_1": "Kineton House, 31 Horsefair",
  "restaurant_address_2": "Banbury",
  "restaurant_address_3": "Oxfordshire",
  "restaurant_post_code": "OX16 0AE",
  "restaurant_country_code": "GB",
  "restaurant_lat": 52.0607,
  "restaurant_lng": 1.33956,

  "restaurant_telephone": "+44 7734038999",
  "restaurant_email": "info@restaurantcollective.org.uk",
  "restaurant_website": "https://restaurantcollective.org.uk",
  "restaurant_spw_url": "https://spw.restaurantcollective.org.uk/92596-rc-demo-restaurant/",
  "restaurant_spw_type": "member",
  
  "restaurant_facebook": "https://faceboook.com/restaurantcollective",
  "restaurant_twitter": "https://twitter.com/RCollectiveUK",
  "restaurant_instagram": "https://instagram.com/restaurantcollectiveuk",
  	
  "restaurant_cuisine_1": "British",
  "restaurant_cuisine_2": "Cafe",
  
  "restaurant_opening_hours": {
  	0: "Sun: Closed all day"
		1: "Mon: 08:00 - 18:00"
		2: "Tue: 08:00 - 18:00"
		3: "Wed: 08:00 - 18:00"
		4: "Thu: 08:00 - 18:00"
		5: "Fri: 08:00 - 18:00"
		6: "Sat: Closed all day"
	},
  "restaurant_opening_notes": "All Year"

  "restaurant_image_cdn": "https://res.cloudinary.com/rdl/image/upload/"
  "restaurant_image_path": "restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg",
  
  "restaurant_attributes": {
  	0: "Children Welcome"
  	1: "Wheelchair Access"
  	2: "Vegetarian Options"
  	3: "Reservations"
  	4: "Internet Booking"
  },
  
  "restaurant_description": "This is for a full description of the restaurant and will primarily be used for display on the restaurants landing page, or Single Page Website (SPW). This description can be used to describe the restaurant's style, cuisine, ethos, ambience, decor, location etc. in much greater detail, and to highlight its key features. It can be up to 5000 characters in length.",
  
  "restaurant_last_updated": "2019-06-13T09:45:14.000Z",
}
```

### Responsive image examples

Images are served by the Cloudinary CDN and can be requested at any size. An `https` request can be constructed as follows:

 - **Originally uploaded image**

```
<restaurant_image_cdn> + <restaurant_image_path>
```
e.g. [https://res.cloudinary.com/rdl/image/upload/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg](https://res.cloudinary.com/rdl/image/upload/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg)
 - **400 x 300px image** (centre cropped/filled)

```
<restaurant_image_cdn> + 'c_fill,w_400,h_300' + <restaurant_image_path>
```
e.g. [https://res.cloudinary.com/rdl/image/upload/c_fill,w_400,h_300/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg](https://res.cloudinary.com/rdl/image/upload/c_fill,w_400,h_300/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg)

 - **Square 120px thumbnail image**  (centre cropped/filled)

```v1649075679/restaurants/<restaurant_number>/<restaurant_image>
<restaurant_image_cdn> + 'c_fill,w_120,h_120' + <restaurant_image_path>
```
e.g. [https://res.cloudinary.com/rdl/image/upload/c_fill,w_120,h_120/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg](https://res.cloudinary.com/rdl/image/upload/c_fill,w_120,h_120/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg)

