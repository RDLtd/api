# Restaurant Detail

Returns the detailed data set for restaurant, including images, menus, and other associated data 

* **URL**

  `https://api.restaurantcollective.io/api/restaurant_detail`

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
    restaurant_detail : restaurant_detail,
    status: 'OK',
    accessed: now,
    info : {
        "version": "V1.1beta",
        "release": "28/04/22",
        "tag": "RDL-API"
    }
}
```
Where *restaurant_detail* is a JSON structure that contains all currently available data for a restaurant (values in bold should always be returned):

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
- **spw_type** *string* [ member | curated | stock ]
- facebook *string*
- twitter *string*
- instagram *string*
- **opening_hours** 
- **cuisine_1** *string*
- cuisine_2 *string*
- **image_cdn:** *string*
- **default_image_path:** *string*
- **opening_hours** *object*
- opening_notes *string*
- **attributes:** *object*
- **description** *string*
- **strap_line** *string*
- **one_sentence** *string*
- **one_paragraph** *string*
- **booking_policy** *string*
- group_policy *string*
- private_dining *string*
- public_transport *string*
- parking *string*
- images *object*
- download_menus *object*
- sections *object*
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
      'https://api.restaurantcollective.io/api/restaurant_detail', true);
      xhr_bkg_request.setRequestHeader('Content-Type', 'application/json;charset=UTF-8');
      xhr_bkg_request.send(JSON.stringify(api_params));
```

* **Angular / TypeScript**

As would appear in an Angular service

```
 getRestaurantDetail(user_code, api_key, restaurant_number) {
    return this.http.post('https://api.restaurantcollective.io/api/restaurant_detail',
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
    restaurant_number : 'EN044999999'
}
```
returns *restaurant_detail*:

```
{
  "number": "EN03392596",
  "group_name": "RDL",
  "name": "RC Demo Restaurant",
  
  "address_1": "Kineton House, 31 Horsefair",
  "address_2": "Banbury",
  "address_3": "Oxfordshire",
  "post_code": "OX16 0AE",
  "country_code": "GB",
  "lat": 52.0607,
  "lng": 1.33956,

  "telephone": "+44 7734038999",
  "email": "info@restaurantcollective.org.uk",
  "website": "https://restaurantcollective.org.uk",
  "spw_url": "https://spw.restaurantcollective.org.uk/92596-rc-demo-restaurant/",
  "spw_type": "member",
  
  "facebook": "https://faceboook.com/restaurantcollective",
  "twitter": "https://twitter.com/RCollectiveUK",
  "instagram": "https://instagram.com/restaurantcollectiveuk",
  	
  "cuisine_1": "British",
  "cuisine_2": "Cafe",
  
  "opening_hours": {
  	0: "Sun: Closed all day"
	1: "Mon: 08:00 - 18:00"
	2: "Tue: 08:00 - 18:00"
	3: "Wed: 08:00 - 18:00"
	4: "Thu: 08:00 - 18:00"
	5: "Fri: 08:00 - 18:00"
	6: "Sat: Closed all day"
  },
  "opening_notes": "All Year"

  "image_cdn": "https://res.cloudinary.com/rdl/image/upload/"
  "default_image_path": "restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg",
  
  "attributes": {
  	0: "Children Welcome"
  	1: "Wheelchair Access"
  	2: "Vegetarian Options"
  	3: "Reservations"
  	4: "Internet Booking"
  },
  
  "description": "This is for a full description of the restaurant and will primarily be used for display on the restaurants landing page, or Single Page Website (SPW). This description can be used to describe the restaurant's style, cuisine, ethos, ambience, decor, location etc. in much greater detail, and to highlight its key features. It can be up to 5000 characters in length.",

  strap_line: "An optional subtitle",
  one_sentence: "This should be a single sentence, highlighting the main features of the restaurant.",
  one_paragraph: "The one-paragraph description of the restaurant may be used independently, for listings, or as a 'lead' paragraph to the full description.",
  booking_policy: "This section provides some general information and instructions about reservations. If the restaurant takes online bookings, then the booking widget below connects to the provider",
  group_policy: "If the restaurant accepts large group or party bookings, then information and contact details can be added here.",
  private_dining: "This section describes any private dining facilities that the restaurant may have, such as private rooms or vip areas.",
  public_transport: "Provide details of any public transport facilities that are close by, stations, bus routes etc.",
  parking: "If there is car parking options nearby, then you can add them here.",
  images: {
    0: {
      image_path: 'restaurants/EN03392596/i1tw0w59iplkvn1xw1tm.jpg'
    }
    1: {
      image_path: 'restaurants/EN03392596/gohsy0y0px96f2jofs2r.jpg'
    }
    2: { 
      image_path: 'restaurants/EN03392596/ql4kyfak10hqfyqngopq.jpg'
    }
    3: { 
      image_path: 'restaurants/EN03392596/zkowtue4awvfortsljp6.jpg'
    }
    4: {
      image_path: 'restaurants/EN03392596/brqv6jikjiucvlqdos1h.jpg'
    }
    5: {
      image_path: 'restaurants/EN03392596/dbh7yg82buiqmrfbamny.jpg'
    }
  }
  download_menus: {
    0: "https://res.cloudinary.com/rdl/image/upload/v1649079789/restaurants/EN03392596/qfdekhcp1pplslf2etby.pdf"
  }
  sections: {
    0:
      dishes: Array(6)
        0: {
          name: 'PATÉ DI FEGATINI', 
          description: 'Home-made Chicken Liver Paté served with Rustic Sicilian Bread and Relish.', 
          price: '6.25', 
          vegetarian: 0, 
          gluten_free: 0,
          vegan: 0
        }
        1: {
          name: 'INSALATA CAPRESE GF', 
          description: 'Sliced Beef Tomato, Mozzarella and Rocket with a d…of Virgin Olive Oil and Oregano / or with Avocado', 
          price: '6.00', 
          vegetarian: 1, 
          gluten_free: 0,
          vegan: 0
        }
        2: {
          name: 'GRIGLIATA DI ORTAGGI E VERDURE', 
          description: 'Grilled mixed Vegetables marinated in Extra Virgin Olive Oil and Vinegar', 
          price: '6.00', 
          vegetarian: 1, 
          gluten_free: 1, 
          vegan: 0
        }
        3: {
          name: 'SPAGHETTI ALLE VONGOLE', 
          description: 'Fresh Clams, Garlic, little Chilli, Extra Virgin Olive Oil (with or without Tomato Sauce)', 
          price: '12.50', 
          vegetarian: 0, 
          gluten_free: 0, 
          vegan: 0
        }
        4: {
          name: "AGNOLOTTI D'AGNELLO", 
          description: 'Homemade Pasta Parcels filled with young Welsh Lam…Velvety Red Wine, fresh Rosemary and Garlic Sauce', 
          price: '13.00', 
          vegetarian: 0, 
          gluten_free: 0, 
          vegan: 0
        }
        5: {
          name: 'LINGUINE MONTALBANO', 
          description: 'Pasta with half dozen of King Prawns, Garlic, Chilli and little bit of Tomato Sauce', 
          price: '11.75', 
          vegetarian: 0, 
          gluten_free: 0, 
          vegan: 0
        }
      name: "SAMPLE DISHES"
  }
  
  "last_updated": "2019-06-13T09:45:14.000Z",
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

