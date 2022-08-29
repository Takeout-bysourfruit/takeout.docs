<p align='center'><img src="https://i.ibb.co/s9kq3V0/takeout.png" height="150px"/></p>
<h1 align='center'>Takeout.docs</h1>
<p align='center'>Takeout.docs is a repository of documentation for various Takeout libraries, as well as documentation for the API.</p>


## JavaScript 🔗
You can find the docs for Takeout.js **[here](https://github.com/Takeout-bysourfruit/takeout.js)**. 

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



*It should be noted that a body is not required. It should also be noted that if you provide both text & HTML, your HTML will be prioritised and sent. Use of an 'official' client is recommended, due to its 'read from file' functionality. You could, of course, implement this yourself.

**There are more endpoints, mainly either used by Takeout.web, or they're just not ready for public use. Examples include email verification via SMTP, getting an archive of any emails sent by you within the last 48 hours, and more. This functionality might be available in the clients, or in the Takeout Dashboard.
