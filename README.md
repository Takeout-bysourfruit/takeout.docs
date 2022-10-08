<p align='center'><img src="https://i.ibb.co/s9kq3V0/takeout.png" height="150px"/></p>
<h1 align='center'>Takeout.docs</h1>
<p align='center'>Takeout.docs is a repository of documentation for various Takeout libraries, as well as documentation for the API.</p>


## JavaScript 🔗
You can find the docs for Takeout.js **[here](https://github.com/Takeout-bysourfruit/takeout.js)**. 

Here's a more "blog"-style **[dev.to post](https://dev.to/takeout/getting-started-with-takeout-using-nodejs-5407)** which helps you get started with Takeout. 

## Python 🔗
You can find the docs for Takeout.py **[here](https://github.com/Takeout-bysourfruit/takeout.py)**. 

## Using the API 💻
You can access the API at **[takeout.bysourfruit.com/api/](https://takeout.bysourfruit.com/api/)** (this'll throw a 404). 

Whether you'd like to use the API, Takeout.js, Takeout.py, et al. you need to provide a token. 
Your token is found in the **[dashboard](https://takeout.bysourfruit.com/dashboard)**, and is generated upon sign up.

Technically, the **only** endpoint you need when using the API yourself is **[takeout.bysourfruit.com/api/email/send](https://takeout.bysourfruit.com/api/email/send)**, 
which, as I hope you guessed, is the POST endpoint to send an email. 

To use it, you need to provide a few things, listed in this table: 

| JSON   | Function  | Is required?  |
|---|---|---|
| sender | Who's the email sending from | Yes |
| receiver  | Who you're sending this email to  | Yes |
| subject  | Your email's subject  | Yes |
| bodyText  | Your email's body (text)  | No, if you provided bodyHTML* |
| bodyHTML  | Your email's body (HTML)  | No, if you provided bodyText* |

To actually authenticate yourself, pass your token as "Token [YOUR TOKEN HERE]" - similar to "Bearer [BEARER]"
| Header | Function | Is required?
|--|--|--|
| Authorization: "Token [YOUR TOKEN]" | Authentication | Yes |

Here's an example using cURL:

```shell
curl -X POST \
  'https://takeout.bysourfruit.com/api/email/send' \
  --header 'Accept: */*' \
  --header 'Authorization: Token YOUR_TOKEN_HERE' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'sender=YOUR_SENDER' \
  --data-urlencode 'receiver=YOUR_RECEIVER' \
  --data-urlencode 'subject=YOUR_SUBJECT' \
  --data-urlencode 'bodyText=YOUR_TEXT_BODY'
  --data-urlencode 'bodyHTML=YOUR_HTML_BODY'
```


*It should be noted that a body is not required. It should also be noted that if you provide both text & HTML, your HTML will be prioritised and sent. Use of an 'official' client is recommended, but not required. 

**There are more endpoints, mainly either used by Takeout's website (e.g to get usage statistics), or they're just not ready for public use. Examples include email verification via SMTP, getting an archive of any emails sent by you within the last 48 hours, and more. This functionality might be available in the clients, or in the Takeout Dashboard.

## Using Webhooks :bell:

Configure Webhooks in the Takeout **[dashboard](https://takeout.bysourfruit.com/dashboard)**, found in the Webhooks tab. Provide Takeout with a URL that's able to receive POST requests, and watch the magic happen. 

Takeout will send JSON similar to this:
```json
{
  "notification": "read", *
  "bounced": false,
  "data": {
    "email": "pika@chu.con", *
    "from": "\"Pikachu\" <takeout@bysourfruit.com>", *
    "wasRead": true,
    "emailID": "123PIKA123"
  }
}
```

Fields marked using an asterisk (\*\) will always be provided with values. Fields without them may sometimes arrive with 'null' , 'unknown' , or 'undefined' instead of usable data.

In your own code, you can filter webhook notifications just by reading the 'notification' value, which will always have 'sent' , 'bounce' or 'read' as a value. When Takeout tests your endpoint, it'll prepend 'test-' to the notification value (e.g 'test-bounce')
