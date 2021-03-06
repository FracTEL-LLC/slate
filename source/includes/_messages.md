# Messages

## Send

> Example Request

```shell
# Send an MMS message "Hello World"
# that does not require confirmation
# from FoneNumber 3215551111
# to a recipent 3215552222
# containing an image https://www.fractel.net/wp-content/uploads/2014/03/FracTEL_Tag_Logo.png
# with a callback url https://hookb.in/vDkMOVB9
$ curl --request POST
--url 'https://api.fonestorm.com/v2/messages/send'
--header 'Content-Type: application/json'
--header 'Accept: application/json'
--header 'token: key'
--data '{"to":"3215552222", "fonenumber": "3215551111", "message": "Hello%20World", "media_url": "https://www.fractel.net/wp-content/uploads/2014/03/FracTEL_Tag_Logo.png", "confirmation_url": "https%3A%2F%2Fhookb.in%2FvDkMOVB9", "require_confirmation": false}'
```

```javascript
// Send an MMS message "Hello World"
// that does not require confirmation
// from FoneNumber 3215551111
// to a recipent 3215552222
// containing an image https://www.fractel.net/wp-content/uploads/2014/03/FracTEL_Tag_Logo.png
// with a callback url https://hookb.in/vDkMOVB9
var FracTelApi = require('frac_tel_api_212');
var apiInstance = new FracTelApi.MessagesApi();
var to = "3215552222";
var fonenumber = "3215551111";
var message = "Hello World";
var opts = {
  'mediaUrl': ["https://www.fractel.net/wp-content/uploads/2014/03/FracTEL_Tag_Logo.png"],
  'confirmationUrl': "https://hookb.in/vDkMOVB9",
  'requireConfirmation': false
};

var callback = function(error, data, response) {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
};
apiInstance.postMessagesSend(to, fonenumber, message, opts, callback);
```

```php
<?php
// Send an MMS message "Hello World"
// that does not require confirmation
// from FoneNumber 3215551111
// to a recipent 3215552222
// containing an image https://www.fractel.net/wp-content/uploads/2014/03/FracTEL_Tag_Logo.png
// with a callback url https://hookb.in/vDkMOVB9
require_once(__DIR__ . '/vendor/autoload.php');

$api_instance = new Swagger\Client\Api\MessagesApi();
$to = "3215552222";
$fonenumber = "3215551111";
$message = "Hello World";
$media_url = array("https://www.fractel.net/wp-content/uploads/2014/03/FracTEL_Tag_Logo.png");
$confirmation_url = "https://hookb.in/vDkMOVB9";
$confirmation_url_username = '';
$confirmation_url_password = '';
$require_confirmation = false;

try {
    $result = $api_instance->postMessagesSend($to, $fonenumber, $message, $media_url, $confirmation_url, $confirmation_url_username, $confirmation_url_password, $require_confirmation);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling MessagesApi->postMessagesSend: ', $e->getMessage(), PHP_EOL;
}
?>
```

```python
# Send an MMS message "Hello World"
# that does not require confirmation
# from FoneNumber 3215551111
# to a recipent 3215552222
# containing an image https://www.fractel.net/wp-content/uploads/2014/03/FracTEL_Tag_Logo.png
# with a callback url https://hookb.in/vDkMOVB9
from __future__ import print_function
import time
import swagger_client
from swagger_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = swagger_client.MessagesApi()
to = '3215552222'
fonenumber = '3215551111'
message = 'Hello World'
media_url = ['https://www.fractel.net/wp-content/uploads/2014/03/FracTEL_Tag_Logo.png']
confirmation_url = 'https://hookb.in/vDkMOVB9'
require_confirmation = false

try:
    # Send an SMS or MMS message to a recipient.
    api_response = api_instance.post_messages_send(to, fonenumber, message, media_url=media_url, confirmation_url=confirmation_url, require_confirmation=require_confirmation)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MessagesApi->post_messages_send: %s\n" % e)
```

> Example Response

```json
{
  "status_code": 200,
  "result": "SUCCESS",
  "uid": "574330d1cdd7e1566b61b771ac72295f"
}
```

Send an SMS or MMS message to a recipient.

### HTTP Request

Method | Route
--------- | -------
**POST** | `/messages/send`

### Body Parameters

Parameter | Type | Default | Description
--------- | ------- | ----------- | -----------
to | string |  | The recipient's 10 digit phone number.
fonenumber | string | | A FoneNumber associated with the account.
message | string | | Contents of the SMS or MMS.
media_url<br/>_optional_ | array[string] | | Valid HTTP or HTTPS URL(s) for media to send via MMS. See **Notes** for additional information.
confirmation_url<br/>_optional_ | string | | Valid HTTP or HTTPS URL that will accept callback data after the message is sent. See **Notes** for additional information.
require_confirmation<br/>_optional_ | string | | Only send message if confirmation is available. See **Notes** for additional information.

### Response Properties

Property | Type | Description
--------- | ------- | -----------
status_code | integer | HTTP status code.
result | string | Text result of the request.
uid | string | Unique identifier of the sent message.

<aside class="notice">
Networks impose a limit of one message per second per sending (<code>from</code>) number. Calls that exceed this rate limit will receive an error code of <code>400 - Rate Limit Exceeded</code>.
</aside>

### Notes

#### `media_url`

Binaries, as identified by `media_url`, have a size limit of 1.5MB.

Multiple entries for `media_url`, with a limit of 10 per message, are supported. If a single URL is being sent, it must be sent as a single-element array.

**Supported MMS File Types**

Extension | File Type | - | Extension | File Type | - | Extension | File Type | - | Extension | File Type
--------- | --------- | - | --------- | --------- | - | --------- | --------- | - | --------- | ---------
.gz | application/gzip | | .flac | audio/flac | | .jpg | image/jpeg | | .avi | video/avi
.js | application/javascript | | .m4a | audio/mp4 | | .pjpeg | image/pjpeg | | .m4v | video/mp4
.json | application/json | | .m4b | audio/mp4 | | .png | image/png | | .mp4 | video/mp4
.oga | application/ogg | | .m4p | audio/mp4 | | .svg | image/svg+xml | | .m1v | video/mpeg
.ogg | application/ogg | | .m4r | audio/mp4 | | .tif | image/tiff | | .mpeg | video/mpeg
.ogv | application/ogg | | .m1a | audio/mpeg | | .tiff | image/tiff | | .mpg | video/mpeg
.ogx | application/ogg | | .m2a | audio/mpeg | | .webp | image/webp | | .mpv | video/mpeg
.pdf | application/pdf | | .mp1 | audio/mpeg | | .ico | image/x-icon | | .ogg | video/ogg
.rtf | application/rtf | | .mp2 | audio/mpeg | | .cal | text/calendar | | .ogm | video/ogg
.smil | application/smil | | .mp3 | audio/mpeg | | .css | text/css | | .ogv | video/ogg
.bz2 | application/x-bzip2 | | .mpa | audio/mpeg | | .csv | text/csv | | .ogx | video/ogg
.gz | application/x-gzip | | .oga | audio/ogg | | .html | text/html | | .spx | video/ogg
.tar | application/x-tar | | .wav | audio/wav | | .js | text/javascript | | .mov | video/quicktime
.xml | application/xml | | .webm | audio/webm | | .txt | text/plain | | .qt | video/quicktime
.zip | application/zip | | .bmp | image/bmp | | .vcard | text/vcard | | .webm | video/webm
.3gp | audio/3gpp | | .dib | image/bmp | | .vcf | text/vcard | | .flv | video/x-flv
.3ga | audio/amr | | .gif | image/gif | | .wap | text/vnd.wap.wml | | .wmv | video/x-ms-wmv
.amr | audio/amr | | .jpeg | image/jpeg | | .xml | text/xml

#### `confirmation_url`

Message sending confirmation callback URLs receive JSON data via a `POST` request (see below for a description of the data package) but can also use token replacements to receive callback data values in query string parameters. For example, the following partial query string maps each callback data value to parameters in the query string: `recipient={{to}}&sender={{from}}&message={{msg}}&code={{dc}}&state={{ds}}&id={{uid}}`

Parameter | Type | Default | Description
--------- | ------- | ----------- | -----------
to | string | | Phone number of recipient.
from | string | | FoneNumber of sender.
message | string | | Contents of the message.
deliverystate | string | | Delivery state of the message. Potential values are `waiting`, `delivered` or  `not-delivered`.
deliverycode | int | | Delivery code of the message. Potential values are: <ul><li>`000` - Message delivered to carrier</li><li>`100` - Message not delivered to carrier</li><li>`187` - Statistical spam detected</li><li>`188` - Keyword spam detected</li><li>`189` - Spam detected</li><li>`482` - Loop detected</li><li>`600` - Destination carrier could not accept messages</li><li>`610` - Message submission failed</li><li>`620` - Destination application error</li><li>`630` - Message not acknowledged</li><li>`720` - Invalid destination number</li><li>`740` - Invalid source number</li><li>`999` - Unknown error</li></ul>
uid | string | | Unique identifier for the message.

#### `require_confirmation`

If this is set to `false`, and a message cannot be delivered with a confirmation option, the API will send the message anyway. This is the default behavior if this parameter is omitted.

If this is set to `true`, and a message cannot be delivered with a confirmation option, the API will return an error and the message will NOT be sent.

<aside class="notice">
Sending messages may result in additional charges and fees to your account.
</aside>

## Send Notify

> Example Request

```shell
# Configure FoneNumber 3215551111 to receive a callback with
# POST data (application/x-www-form-urlencoded) to url https://hookb.in/vDkMOVB9
# when a message is sent.
curl --request POST
--url 'https://api.fonestorm.com/v2/messages/send_notify'
--header 'Content-Type: application/json'
--header 'Accept: application/json'
--header 'token: key'
--data '{"fonenumber":"3215551111", "method":"POST", "url": "https%3A%2F%2Fhookb.in%2FvDkMOVB9" }'
```

```javascript
// Configure FoneNumber 3215551111 to receive a callback with
// POST data (application/x-www-form-urlencoded) to url https://hookb.in/vDkMOVB9
// when a message is sent.
var FracTelApi = require('frac_tel_api_212');
var apiInstance = new FracTelApi.MessagesApi();
var fonenumber = "3215551111";
var method = "POST";
var url = "https://hookb.in/vDkMOVB9";
var opts = {};

var callback = function(error, data, response) {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
};
apiInstance.postMessagesSendNotify(fonenumber, method, url, opts, callback);
```

```php
<?php
// Configure FoneNumber 3215551111 to receive a callback with
// POST data (application/x-www-form-urlencoded) to url https://hookb.in/vDkMOVB9
// when a message is sent.
require_once(__DIR__ . '/vendor/autoload.php');

$api_instance = new Swagger\Client\Api\MessagesApi();
$fonenumber = "3215551111";
$method = "POST";
$url = "https://hookb.in/vDkMOVB9";

try {
    $result = $api_instance->postMessagesSendNotify($fonenumber, $method, $url);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling MessagesApi->postMessagesSendNotify: ', $e->getMessage(), PHP_EOL;
}
?>
```

```python
# Configure FoneNumber 3215551111 to receive a callback with
# POST data (application/x-www-form-urlencoded) to url https://hookb.in/vDkMOVB9
# when a message is sent.
from __future__ import print_function
import time
import swagger_client
from swagger_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = swagger_client.MessagesApi()
fonenumber = '3215551111'
method = 'POST'
url = 'https://hookb.in/vDkMOVB9'

try:
    # Configure the callback URL to notify when a message is sent.
    api_response = api_instance.post_messages_send_notify(fonenumber, method, url)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MessagesApi->post_messages_send_notify: %s\n" % e)
```

> Example Response

```json
{
  "status_code": 200,
  "result": "SUCCESS"
}
```

Configure the callback URL to notify when a message is sent. Each FoneNumber can be configured to use its own callback URL for handling send notifications.

### HTTP Request

Method | Route
--------- | -------
**POST** | `/messages/send_notify`

### Body Parameters

Parameter | Type | Default | Description
--------- | ------- | ----------- | -----------
fonenumber | string |  | A FoneNumber associated with the account.
url | string | | Callback URL. See **Notes** for additional information.
method | string | | Allowed values are `GET`,`POST`, or `JSON`. See **Notes** for additional information.

### Response Properties

Property | Type | Description
--------- | ------- | -----------
status_code | integer | HTTP status code.
result | string | Text result of the request.

### Notes

#### `url`

This is a valid HTTP or HTTPS URL that will accept callback data when a message is sent from the FoneNumber specified in `from`.

#### `method`

One of three available methods must be specified for the callback execution.

- `GET` returns data through query string parameters on a `GET` to the given URL.
- `POST` returns data as _(application/x-www-form-urlencoded)_ in the body of a `POST` to the given URL.
- `JSON` returns data as _(application/json)_ in the body of a `POST` to the given URL.

#### Callback Data

Parameter | Type | Default | Description
--------- | ------- | ----------- | -----------
to | string | | Phone number of recipient.
from | string | | FoneNumber of sender.
message | string | | Contents of the message.
uid | string | | Unique identifier for the message.

Callback URLs using the `GET` method use token replacements to place callback data values in query string parameters. For example, the following partial query string maps each callback data value to parameters in the query string: `recipient={{to}}&sender={{from}}&message={{msg}}&id={{uid}}`

## Receive

> Example Request

```shell
# Deliver all messages received by FoneNumber 3215551111
# to an email address email@domain.
$ curl --request POST
--url 'https://api.fonestorm.com/v2/messages/receive'
--header 'Content-Type: application/json'
--header 'Accept: application/json'
--header 'token: key'
--data '{"fonenumber": "3215551111", "type": "Email", "value": "email@domain.com"}'
```

```javascript
// Deliver all messages received by FoneNumber 3215551111
// to an email address email@domain.
var FracTelApi = require('frac_tel_api_212');
var apiInstance = new FracTelApi.MessagesApi();
var fonenumber = "3215551111";
var type = "Email";
var opts = {
  'value': "email@domain.com"
};

var callback = function(error, data, response) {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
};
apiInstance.postMessagesReceive(fonenumber, type, opts, callback);
```

```php
<?php
// Deliver all messages received by FoneNumber 3215551111
// to an email address email@domain.
require_once(__DIR__ . '/vendor/autoload.php');

$api_instance = new Swagger\Client\Api\MessagesApi();
$fonenumber = "3215551111";
$type = "Email";
$value = "email@domain.com";

try {
    $result = $api_instance->postMessagesReceive($fonenumber, $type, $value);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling MessagesApi->postMessagesReceive: ', $e->getMessage(), PHP_EOL;
}
?>
```

```python
# Deliver all messages received by FoneNumber 3215551111
# to an email address email@domain.
from __future__ import print_function
import time
import swagger_client
from swagger_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = swagger_client.MessagesApi()
fonenumber = '3215551111'
type = 'Email'
value = 'email@domain.com'

try:
    # Configure the delivery service type used as the destination for received messages.
    api_response = api_instance.post_messages_receive(fonenumber, type, value=value, url_method=url_method, url_username=url_username, url_password=url_password)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MessagesApi->post_messages_receive: %s\n" % e)
```

> Example Response

```json
{
  "status_code": 200,
  "result": "SUCCESS"
}
```

Configure the delivery service type used as the destination for received messages.

### HTTP Request

Method | Route
--------- | -------
**POST** | `/messages/receive`

### Body Parameters

Parameter | Type | Default | Description
--------- | ------- | ----------- | -----------
fonenumber | string |  | A FoneNumber associated with the account.
type | string | | Message service routing type. Allowed values are `Device`, `Email`, `URL`, `Forward`, or `None`. See **Notes** for additional information.
value | string | | Value of the chosen message routing type. Allows for a _Device ID_, _Email Address_, _URL_, or _Phone Number_ depending on the specified `type`. See **Notes** for additional information.

### Response Properties

Property | Type | Description
--------- | ------- | -----------
status_code | integer | HTTP status code.
result | string | Text result of the request.

### Notes

#### `type`

Incoming messages can be routed to one of several destination options: a configured and registered `Device` (e.g. SIP handset, Fractelfone mobile app, or WebRTC endpoint), a valid `Email` address, a callback `URL`, or `Forward` to another telephone number. There is also the option to set the destination to `None`, in which case messages are deleted upon receipt without any delivery. Use the `type` parameter to specify the type of destination.

#### `value`

The `value` parameter contains the corresponding setting for the destination.

Type | Value | Example
------ | ------- | --------
Device | The ID for the destination device | 987123543678
Email  | An email address                  | bingo@stokes.com
URL    | A callback URL                    | https://api.yourserver.com/handler.php?msg={{msg}}
Forward | A forwarding phone number        | 3215551111
None    | _None_                           |

#### Callback Data

Parameter | Type | Default | Description
--------- | ------- | ----------- | -----------
to | string | | FoneNumber of recipient.
from | string | | Phone number of sender.
message | string | | Contents of the message.
uid | string | | Unique identifier for the message.

Callback URLs use the `POST` method and use token replacements to place callback data values in query string parameters. For example, the following partial query string maps each callback data value to parameters in the query string: `recipient={{to}}&sender={{from}}&message={{msg}}&id={{uid}}`

## Receive Notify

> Example Request

```shell
# Configure FoneNumber 3215551111 to receive a callback with
# JSON payload data (application/json) to url https://hookb.in/vDkMOVB9
# when a message is received.
$ curl --request POST
--url 'https://api.fonestorm.com/v2/messages/receive_notify'
--header 'Content-Type: application/json'
--header 'Accept: application/json'
--header 'token: key'
--data '{"fonenumber": "3215551111", "method": "JSON", "url": "https%3A%2F%2Fhookb.in%2FvDkMOVB9"}'
```

```javascript
// Configure FoneNumber 3215551111 to receive a callback with
// JSON payload data (application/json) to url https://hookb.in/vDkMOVB9
// when a message is received.
var FracTelApi = require('frac_tel_api_212');
var apiInstance = new FracTelApi.MessagesApi();
var fonenumber = "3215551111";
var method = "JSON";
var url = "https://hookb.in/vDkMOVB9";
var opts = {};

var callback = function(error, data, response) {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
};
apiInstance.postMessagesReceiveNotify(fonenumber, method, url, opts, callback);
```

```php
<?php
// Configure FoneNumber 3215551111 to receive a callback with
// JSON payload data (application/json) to url https://hookb.in/vDkMOVB9
// when a message is received.
require_once(__DIR__ . '/vendor/autoload.php');

$api_instance = new Swagger\Client\Api\MessagesApi();
$fonenumber = "3215551111";
$method = "JSON";
$url = "https://hookb.in/vDkMOVB9";

try {
    $result = $api_instance->postMessagesReceiveNotify($fonenumber, $method, $url);
    print_r($result);
} catch (Exception $e) {
    echo 'Exception when calling MessagesApi->postMessagesReceiveNotify: ', $e->getMessage(), PHP_EOL;
}
?>
```

```python
# Configure FoneNumber 3215551111 to receive a callback with
# JSON payload data (application/json) to url https://hookb.in/vDkMOVB9
# when a message is received.
from __future__ import print_function
import time
import swagger_client
from swagger_client.rest import ApiException
from pprint import pprint

# create an instance of the API class
api_instance = swagger_client.MessagesApi()
fonenumber = '3215551111'
method = 'JSON'
url = 'https://hookb.in/vDkMOVB9'

try:
    # Configure the callback URL to notify when a message is received.
    api_response = api_instance.post_messages_receive_notify(fonenumber, method, url)
    pprint(api_response)
except ApiException as e:
    print("Exception when calling MessagesApi->post_messages_receive_notify: %s\n" % e)
```

> Example Response

```json
{
  "status_code": 200,
  "result": "SUCCESS"
}
```

Configure the callback URL to notify when a message is received. Each FoneNumber can be configured to use its own callback URL for handling receive notifications.

### HTTP Request

Method | Route
--------- | -------
**POST** | `/messages/receive_notify`

### Body Parameters

Parameter | Type | Default | Description
--------- | ------- | ----------- | -----------
fonenumber | string |  | A FoneNumber associated with the account.
url | string | | Callback URL. See **Notes** for additional information.
method | string | | Allowed values are `GET`,`POST`, or `JSON`. See **Notes** for additional information.

### Response Properties

Property | Type | Description
--------- | ------- | -----------
status_code | integer | HTTP status code.
result | string | Text result of the request.

### Notes

#### `url`

This is a valid HTTP or HTTPS URL that will accept callback data when a message is sent to the FoneNumber specified in `fonenumber`.

#### `method`

One of three available methods must be specified for the callback execution.

- `GET` returns data through query string parameters on a `GET` to the given URL.
- `POST` returns data as _(application/x-www-form-urlencoded)_ in the body of a `POST` to the given URL.
- `JSON` returns data as _(application/json)_ in the body of a `POST` to the given URL.

#### Callback Data

Parameter | Type | Default | Description
--------- | ------- | ----------- | -----------
to | string | | FoneNumber of recipient.
from | string | | Phone number of sender.
message | string | | Contents of the message.
uid | string | | Unique identifier for the message.

Callback URLs using the `GET` method use token replacements to place callback data values in query string parameters. For example, the following partial query string maps each callback data value to parameters in the query string: `recipient={{to}}&sender={{from}}&message={{msg}}&id={{uid}}`
