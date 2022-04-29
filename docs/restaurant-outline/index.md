# Restaurant Outline

Returns the outline data set for restaurant (core plus a subset suitable for a listing)

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
    * your_number (string) - as specified by RDL
    
    

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
- **opening_hours** 
- **cuisine_1** *string*
- cuisine_2 *string*
- **image_cdn:** *string*
- **default_image_path:** *string*
- **opening_hours:** *object*
- opening_notes: *string*
- **attributes:** *object*
- **description** *string*
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
      channel_access_api_key : '(your_api_key)', 
      restaurant_number : 'EN044999999'
    };

    let xhr_bkg_request = new XMLHttpRequest();
    xhr_bkg_request.open('POST',
      'https://api.restaurantcollective.io/api/outline', true);
      xhr_bkg_request.setRequestHeader('Content-Type', 'application/json;charset=UTF-8');
      xhr_bkg_request.send(JSON.stringify(api_params));
```

* **Angular / TypeScript**

As would appear in an Angular service

```
 getRestaurantOutline(user_code, api_key, number) {
    return this.http.post('https://api.restaurantcollective.io/api/restaurant_outline',
      { 
        channel_access_code : '(your_user_code)',
        channel_access_api_key : '(your_api_key)', 
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
    channel_access_code : 'TT9999',
    channel_access_api_key : 'TESTAPIKEYASISSUEDBYRDLBYCHANNEL'
    number : 'EN044999999'
}
```
returns *restaurant_outline*:

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
  
  opening_hours: {
  	0: "Sun: Closed all day"
	1: "Mon: 08:00 - 18:00"
	2: "Tue: 08:00 - 18:00"
	3: "Wed: 08:00 - 18:00"
	4: "Thu: 08:00 - 18:00"
	5: "Fri: 08:00 - 18:00"
	6: "Sat: Closed all day"
  },
  opening_notes: "All Year"

  image_cdn: "https://res.cloudinary.com/rdl/image/upload/"
  default_image_path: "restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg",
  
  attributes: {
  	0: "Children Welcome"
  	1: "Wheelchair Access"
  	2: "Vegetarian Options"
  	3: "Reservations"
  	4: "Internet Booking"
  },
  
  description: "This is for a full description of the restaurant and will primarily be used for display on the restaurants landing page, or Single Page Website (SPW). This description can be used to describe the restaurant's style, cuisine, ethos, ambience, decor, location etc. in much greater detail, and to highlight its key features. It can be up to 5000 characters in length.",
  
  last_updated: "2019-06-13T09:45:14.000Z",
}
```

### Responsive image examples

Images are served by the Cloudinary CDN and can be requested at any size. An `https` request can be constructed as follows:

 - **Originally uploaded image**

```
<image_cdn> + <image_path>
```
e.g. [https://res.cloudinary.com/rdl/image/upload/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg](https://res.cloudinary.com/rdl/image/upload/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg)
 - **400 x 300px image** (centre cropped/filled)

```
<image_cdn> + 'c_fill,w_400,h_300' + <image_path>
```
e.g. [https://res.cloudinary.com/rdl/image/upload/c_fill,w_400,h_300/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg](https://res.cloudinary.com/rdl/image/upload/c_fill,w_400,h_300/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg)

 - **Square 120px thumbnail image**  (centre cropped/filled)

```
<image_cdn> + 'c_fill,w_120,h_120' + <image_path>
```
e.g. [https://res.cloudinary.com/rdl/image/upload/c_fill,w_120,h_120/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg](https://res.cloudinary.com/rdl/image/upload/c_fill,w_120,h_120/restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg)

