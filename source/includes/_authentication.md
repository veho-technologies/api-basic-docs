# Authentication

> To authenticate a POST request to /packages, use this code:

```javascript
import request from 'request';

function signRequestOptions(options) {
  // make sure headers object exists
  options.headers = options.headers || {};

  // put apiKey in header
  options.headers['apiKey'] = `00000000-0000-0000-0000-000000000000`;

  return options;
}

const client = request.defaults({ baseUrl: 'https://api-basic.shipveho.com/v1' });

const myData = { /* ... */ };

const options = signRequestOptions({
  method: 'POST',
  uri: '/packages',
  body: JSON.stringify(myData),
});

client(options, (err, response, body) => {
  if (err) {
    console.error('request failed', err);
  } else if (response.statusCode >= 400) {
    console.error('an error occurred', body);
  } else {
    // process body
  }
});
```

The Veho Basic API requires an API key provided by Veho to access any endpoint.

Veho expects for the signature to be included in all API requests to the server in a header that looks like the following:

`apiKey: 00000000-0000-0000-0000-000000000000`
