---
author: laujan
ms.service: cognitive-services
ms.subservice: translator-text
ms.topic: include
ms.date: 08/06/2019
ms.author: lajanuar
ms.custom: devx-track-js
---

[!INCLUDE [Prerequisites](prerequisites-nodejs.md)]

[!INCLUDE [Setup and use environment variables](setup-env-variables.md)]

## Create a project and import required modules

Create a new project using your favorite IDE or editor. Then copy this code snippet into your project in a file named `detect.js`.

```javascript
const request = require('request');
const uuidv4 = require('uuid/v4');
```

> [!NOTE]
> If you haven't used these modules you'll need to install them before running your program. To install these packages, run: `npm install request uuidv4`.

These modules are required to construct the HTTP request, and create a unique identifier for the `'X-ClientTraceId'` header.

## Set the subscription key and endpoint

This sample will try to read your Translator subscription key and endpoint from these environment variables: `TRANSLATOR_TEXT_SUBSCRIPTION_KEY` and `TRANSLATOR_TEXT_ENDPOINT`. If you're not familiar with environment variables, you can set `subscriptionKey` and `endpoint` as strings and comment out the conditional statements.

Copy this code into your project:

```javascript
var key_var = 'TRANSLATOR_TEXT_SUBSCRIPTION_KEY';
if (!process.env[key_var]) {
    throw new Error('Please set/export the following environment variable: ' + key_var);
}
var subscriptionKey = process.env[key_var];
var endpoint_var = 'TRANSLATOR_TEXT_ENDPOINT';
if (!process.env[endpoint_var]) {
    throw new Error('Please set/export the following environment variable: ' + endpoint_var);
}
var endpoint = process.env[endpoint_var];
```

## Configure the request

The `request()` method, made available through the request module, allows us to pass the HTTP method, URL, request params, headers, and the JSON body as an `options` object. In this code snippet, we'll configure the request:

```javascript
let options = {
    method: 'POST',
    baseUrl: endpoint,
    url: 'detect',
    qs: {
      'api-version': '3.0',
    },
    headers: {
      'Ocp-Apim-Subscription-Key': subscriptionKey,
      'Content-type': 'application/json',
      'X-ClientTraceId': uuidv4().toString()
    },
    body: [{
          'text': 'Salve, mondo!'
    }],
    json: true,
};
```
The easiest way to authenticate a request is to pass in your subscription key as an
`Ocp-Apim-Subscription-Key` header, which is what we use in this sample. As an alternative, you can exchange your subscription key for an access token, and pass the access token along as an `Authorization` header to validate your request.

If you are using a Cognitive Services multi-service subscription, you must also include the `Ocp-Apim-Subscription-Region` in your request headers.

For more information, see [Authentication](../reference/v3-0-reference.md#authentication).

## Make the request and print the response

Next, we'll create the request using the `request()` method. It takes the `options` object that we created in the previous section as the first argument, then prints the prettified JSON response.

```javascript
request(options, function(err, res, body){
    console.log(JSON.stringify(body, null, 4));
});
```

>[!NOTE]
> In this sample, we're defining the HTTP request in the `options` object. However, the request module also supports convenience methods, like `.post` and `.get`. For more information, see [convenience methods](https://github.com/request/request#convenience-methods).

## Put it all together

That's it, you've put together a simple program that will call the Translator and return a JSON response. Now it's time to run your program:

```console
node detect.js
```

## Sample response

After you run the sample, you should see the following printed to terminal:

> [!NOTE]
> Find the country/region abbreviation in this [list of languages](../language-support.md).

```json
[
    {
        "alternatives": [
            {
                "isTranslationSupported": true,
                "isTransliterationSupported": false,
                "language": "pt",
                "score": 1.0
            },
            {
                "isTranslationSupported": true,
                "isTransliterationSupported": false,
                "language": "en",
                "score": 1.0
            }
        ],
        "isTranslationSupported": true,
        "isTransliterationSupported": false,
        "language": "it",
        "score": 1.0
    }
]
```

## Clean up resources

If you've hardcoded your subscription key into your program, make sure to remove the subscription key when you're finished with this quickstart.

## Next steps

Take a look at the API reference to understand everything you can do with the Translator.

> [!div class="nextstepaction"]
> [API reference](../reference/v3-0-reference.md)