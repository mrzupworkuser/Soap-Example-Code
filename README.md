### installation
To use the client manually, include the CyberSource client in your project:

```php
require_once('/path/to/project/lib/CybsSoapClient.php');
``` 

## Getting Started
The PHP client will generate the request message headers for you, and will contain the methods specified by the WSDL file.

### Creating a simple request
The main method you'll use is ````runTransaction()````. To run a transaction, you'll first need to construct a client to generate a request object, which you can populate with the necessary fields for sample requests. The object will be converted into XML, so the properties of the object will need to correspond to the correct XML format.

```php
$client = new CybsSoapClient();
$request = $client->createRequest();

$card = new stdClass();
$card->accountNumber = '4111111111111111';
$card->expirationMonth = '12';
$card->expirationYear = '2020';
$request->card = $card;

// Populate $request here with other necessary properties

$reply = $client->runTransaction($request);
```

### Creating a request from XML
You can create a request from XML either in a file or from an XML string. Here's how to run a transaction from an XML file:

```php
$referenceCode = 'your_merchant_reference_code';
$client = new CybsSoapClient();
$reply = $client->runTransactionFromFile('path/to/my.xml', $referenceCode);
```

Or, you can create your own XML string and use that instead: 

```php
$xml = "";
// Populate $xml
$client = new CybsSoapClient();
$client->runTransactionFromXml($xml);
```

```php
$client = new CybsNameValuePairClient();
$request = array();
$request['ccAuthService_run'] = 'true';
$request['merchantID'] = 'my_merchant_id';
$request['merchantReferenceCode'] = $'my_reference_code';
// Populate $request
$reply = $client->runTransaction($request);
```
