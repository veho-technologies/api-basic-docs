# Packages


## Create a new package

```javascript
import request from 'request';

const client = request.defaults({ baseUrl: 'https://api-basic.shipveho.com/v1' });

const new_package = {
	destination: {
		street: "1002 Walnut St",
		apartment: "Suite 200",
		city: "Boulder",
		state: "CO",
		zipCode: "80302"
	},
	phone: "555-555-5555",
	recipient: "John Smith",
	instructions: "Leave on front porch behind railing. Beware of dog!",
	serviceClass: "nextDay",
	signatureRequired: "true"
};

const options = signRequestOptions({
  method: 'POST',
  uri: '/packages',
  body: JSON.stringify(new_package),
});

client(options, (err, response, body) => {
  if (err) {
    console.error('request failed', err);
  } else if (response.statusCode >= 400) {
    console.error('error creating package', body);
  } else {
    console.log(`package "${body._id}" created`);
  }
});
```

> The above command returns JSON structured like this:

```json
{
    "_id": "BSG6XZQrgwieFFJPx",
    "destination": {
        "street": "1002 Walnut St",
        "apartment": "Suite 200",
        "city": "Boulder",
        "state": "CO",
        "zipCode": "80302"
    },
    "recipient": "John Smith",
    "phone": "555-555-5555",
    "instructions": "Leave on front porch behind railing. Beware of dog!",
    "serviceClass": "nextDay",
    "signatureRequired": true,
    "scannedByClient": false,
    "createdAt": "2018-07-29T01:09:31.690Z",
    "currentState": "created",
    "barcode": "veho_id_BSG6XZQrgwieFFJPx",
    "customerTrackingLink": "https://tracking.shipveho.com/i/BSG6XZQrgwieFFJPx",
    "zplShippingLabelLink": "https://labels.shipveho.com/zpl/BSG6XZQrgwieFFJPx"
}
```

This endpoint creates a new package. This endpoint should be used by a client upon order completion or fulfillment of an item to notify Veho that there are packages to be shipped, and obtain a barcode and/or shipping label from Veho.

### HTTP Request

`POST https://api-basic.shipveho.com/v1/packages`

### Request body

#### Package Object

Parameter | Type | Description
--------- | ----------- | -----------
destination | `Destination` | address information for delivery (description below)
serviceClass | `string` | requested class of service, currently `sameDay` or `nextDay` (defaults to `nextDay`)
recipient | `string` | full name of the recipient
phone | `string` | `optional` phone number of the recipient (used for SMS)
instructions | `string` | `optional` any additional delivery instructions provided by recipient to assist driver with delivery
signatureRequired | `boolean` | `optional` set to `true` if the recipient has to sign for this packages (defaults to `false`)
externalId | `string` | `optional` any ID you want to have stored with this stop. <br> (f.e. an order number)
width | `integer` | `optional` width of the package, in in
height | `integer` | `optional` height of the package, in in
length | `integer` | `optional` length of the package, in in
weight | `integer` | `optional` weight of the package, in lbs

<aside class="info">
If not declared otherwise, <strong>all parameters are required</strong>.
</aside>

#### Destination object

Destination is an address object in the following shape:

Parameter | Type |  Description
--------- | ----------- | -----------
street | `string` | street address
apartment | `string` | `optional` apartment number, suite number, or any info on the second line of an address
city | `string` | city of the delivery address
zipCode | `string` | ZIP code of the address
state | `string` | state of the address <br> (can be 2 letter postal code, or full state name)
country | `string` | 2 letter ISO country code for the address

<aside class="info">
If not declared otherwise, <strong>all parameters are required</strong>.
</aside>

### Returns

Creating a package object returns the package object, including all the inputted data, addition of any optional data above that has default values, and some additional default and server-generated data:

Parameter | Type |  Description
--------- | ----------- | -----------
currentState | `string` | current state of the package
barCode | `string` | content of the [Code128](https://en.wikipedia.org/wiki/Code_128) bar code the package will have
customerTrackingLink | `string` | mobile tracking link that can be shared with customer
zplShippingLabelLink | `string` | link to zpl shipping label file

## Get a package

```javascript
import request from 'request';

const client = request.defaults({ baseUrl: 'https://api-basic.shipveho.com/v1' });

const options = signRequestOptions({
  method: 'GET',
  uri: '/packages/BSG6XZQrgwieFFJPx'
});

client(options, (err, response, body) => {
  if (err) {
    console.error('request failed', err);
  } else if (response.statusCode >= 400) {
    console.error('error retrieving package', body);
  } else {
    console.log(`package "${body._id}" created`);
  }
});
```

> The above command returns JSON structured like this:

```json
{
    "_id": "BSG6XZQrgwieFFJPx",
    "destination": {
        "street": "1002 Walnut St",
        "apartment": "Suite 200",
        "city": "Boulder",
        "state": "CO",
        "zipCode": "80302"
    },
    "phone": "555-555-5555",
    "recipient": "John Smith",
    "instructions": "Leave on front porch behind railing. Beware of dog!",
    "serviceClass": "nextDay",
    "signatureRequired": true,
    "scannedByClient": false,
    "createdAt": "2018-07-29T02:41:36.151Z",
    "currentState": "created",
    "barcode": "veho_id_BSG6XZQrgwieFFJPx",
    "customerTrackingLink": "https://tracking.shipveho.com/i/BSG6XZQrgwieFFJPx",
    "zplShippingLabelLink": "https://labels.shipveho.com/zpl/BSG6XZQrgwieFFJPx"
}
```

This endpoint retrieves all details of an existing package.

### HTTP Request

`GET https://api-basic.shipveho.com/v1/packages/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | `_id` of the package to retrieve

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------

<aside class="success">
Remember — GET requests must contain an <code>apiKey</code> header.
</aside>
