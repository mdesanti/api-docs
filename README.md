FORMAT: 1A
HOST: http://clients.geartranslations.com/v2

# GT - Quotation V2 API
**Gear Translations Quotation** API to be able to quote different translation files.

## Authentication
Note that every call endpoint expects the token **SESSION_TOKEN** provided by **Gear Translations**

# GT - Quotation V2 API Root [/v2]
API entry point.

# Group Language
Languages resource for the *Gear Translations Quotation*.

## Languages [/languages/valid_from_language]

### Get available from languages [GET]

Languages which are available as an origin language to quote files.

+ Request (application/json)

        {}

+ Response 200

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "valid_languages": [
                    [
                        "English (UK)",
                        30
                    ],
                    [
                        "English (US)",
                        3
                    ],
                    [
                        "Italian",
                        2
                    ],
                    [
                        "German",
                        7
                      ],
                      [
                        "French (France)",
                        4
                    ],
                    [
                        "Portuguese (Brazil)",
                        6
                    ],
                    [
                        "Spanish",
                        1
                    ]
                ]
            }
        
## Languages [/languages/valid_for_origin_language]

### Get available for languages [GET]

Languages which are available as a destination language to quote files according to an origin language.

+ Request (application/json)

        {
            "language_from_id": "1"
        }

+ Response 200

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "valid_languages":[
                    [
                        "English (US)",
                        3
                    ],
                    [
                        "English (UK)",
                        30
                    ],
                    [
                        "Portuguese (Brazil)",
                        6
                    ]
            }
        
# Group Document

Document resource for the *Gear Translations Quotation*.

## File Upload [/documents]

Manage files

### Create [POST]

Upload a file and get its file_id
+ Request (multipart/form-data; boundary=---BOUNDARY)

        -----BOUNDARY
           Content-Disposition: form-data; name="path"; filename="test.txt"
           Content-Type: application/vnd.openxmlformats-officedocument.wordprocessingml.document
           Content-Transfer-Encoding: base64
    
           /9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0a
           HBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIy
           MjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCAABAAEDASIA
           AhEBAxEB/8QAFQABAQAAAAAAAAAAAAAAAAAAAAf/xAAUEAEAAAAAAAAAAAAAAAAAAAAA/8QAFAEB
           AAAAAAAAAAAAAAAAAAAAAP/EABQRAQAAAAAAAAAAAAAAAAAAAAD/2gAMAwEAAhEDEQA/AL+AD//Z
        -----BOUNDARY

+ Response 201

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "files": [
                    {
                        "id": "5427",
                        "name": "500.docx",
                        "size": "500",
                        "url": "/path/13246",
                        "delete_url": "url",
                        "delete_type": "DELETE",
                        "token":"de73ab03256acb1ad16b3aaafe5eca2e200c8fe0"
                    }
                ]
            }
        
## File Delete [/documents/:id]

### Delete [DELETE]

Delete a file by its id

+ Request (application/json)

        {

        }

+ Response 200

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            true

# Group Quotation
Quotation resource for the *Gear Translations Quotation*.

## Conversion Rate [/bulk_quotation/conversion_rate]

Fetch money conversion information according to the user country

 - Conversion Rate: Conversion rate taking USD as a base.
 - Conversin Code: User currency code.
 - Country Name: User country
 
 If the previous information cannot be retrieved from the request, then it returns:
 - Converion Rate: "1.0"
 - Conversion Code: "USD"
 - Country Name: "US"

### Get conversion information [GET]

+ Request (application/json)

        { 
            
        }
          
+ Response 200

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "conversion_rate": "1.0",
                "currency_code": "USD",
                "country_name": "US"
            }
        
## Word Price [/bulk_quotation/word_price]

Fetch the price per word according to the deadline given.
 - deadline_dinamic: Deadline in hours for the translations. "+" is provided if the deadline is after the 48 hours. Others options are 5, 24 and 48.

### Get word price [GET]

+ Request (application/json)

        { 

            "deadline_dinamic": "24"
        }
          
+ Response 200

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "word_price": "0.17"
            }
        
## Coupon Discount [/bulk_quotation/coupon_discount]

Get the discount for a certain coupon code. 
    - Message: Message indicating the error if the discount_code is invalid

### Get coupon discount [GET]

+ Request (application/json)

        {
            "discount_code": "7f013b133f"
        }

+ Response 200

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "coupon_discount": "50.0",
                "coupon_message": ""
            }

# Group Coupon

Coupon resource for the *Gear Translations Quotation*.

## Coupon Creation [/coupons]

Manage coupons

### Create [POST]

Create a coupon for an email. This sends an email with the coupon token for a 30% of discount.
+ Request (application/json)

        {
            "email": "test@example.com"
        }

+ Response 201
    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {}


## Quotation Information [/bulk_quotation/quotation_information]

After uploading the file, this gets the quotation updated information

 - Word Price: "1.0". Same as [/bulk_quotation/word_price]
 - Words Count: Counts the file words
 - deadline_dinamic: Deadline in hours for the translations. "+" is provided if the deadline is after the 48 hours. Others options are 5, 24 and 48.

### Get quotation information [POST]

+ Request (application/json)

        {
            "language_from_id": "1",
            "language_to_id": "[3]",
            "file_id": "13235",
            "deadline_dinamic": "5"
        }

+ Response 200

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "word_price": "0.19",
                "words_count": "370"
            }

## Formal Quotation [/bulk_quotation/formal_quotation]

Pdf with the quotation data

### Get quotation pdf url [POST]

- Url: Url of the formal quotation pdf generated

+ Request (application/json)

        {
            "language_from_id": "1",
            "language_to_id": [1, 6],
            "file-ids": [13236, 13238],
            "comments": "I don't want to translate the second page",
            "discount_code": "7f013b133f",
            "email": "test@example.com",
            "deadline-date": "2014-09-23",
            "deadline-time": "1:15am",
            "time_zone": "Buenos Aires",
            "deadline_dinamic": "48"
        }

+ Response 201

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "url": "url"
            }

## Submit Quotation [/bulk_quotation/submit]

 - Purchase Method: Name of the purchase service
 - Url: Url to go to the purchase service web
 - deadline_dinamic: Deadline in hours for the translations. "+" is provided if the deadline is after the 48 hours. Others options are 5, 24 and 48.

### Finish Quotation [POST]

+ Request (application/json)

        {
            "language_from_id": "1",
            "language_to_id": [1, 6],
            "file-ids": [13236, 13238],
            "comments": "I don't want to translate the second page",
            "discount_code": "7f013b133f",
            "email": "test@example.com",
            "deadline-date": "2014-09-23",
            "deadline-time": "1:15am",
            "time_zone": "Buenos Aires",
            "deadline_dinamic": "48"
        }

+ Response 200

    + Headers

            content-type: application/json; charset=utf-8

    + Body

            {
                "purchase_method": "paypal",
                "url":"url"
            }
