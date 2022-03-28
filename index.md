# Developers Documentation

## How to start?

* Create a development application.
- Once you have created the app, you'll get APP_ID, and APP_SECRET.
Markup :         ![picture](https://www.shoutout.ga/themes/maindesign/img/developer.png)

- To start the Oauth process,use the link https://www.shoutout.ga/oauth?app_id={YOUR_APP_ID}
-  Once the end user clicks this link, he/she will be redirected to the authorization page.
         
- Once the end user authorization the app, he/she will be redirected to your domain name with a GET parameter "code", example: http://yourdomain/?code=XXX
         
- In your code, to retrieve the authorized user info, you need to generate an access code, please use the code below: 
### PHP: ###

```
<?php
	$app_id = 'YOUR_APP_ID'; // your application app id
	$app_secret = 'YOUR_APP_SECRET'; your application app secret
	$code = $_GET['code']; // the GET parameter you got in the callback: http://yourdomain/?code=XXX

	$get = file_get_contents("https://www.shoutout.ga/authorize?app_id={$app_id}&app_secret={$app_secret}&code={$code}");

	$json = json_decode($get, true);
	if (!empty($json['access_token'])) {
		$access_token = $json['access_token']; // your access token
	}
?>
```
- Once you got the access code, simple call the data you would like to retrieve, Example:

PHP:

``` 
if (!empty($json['access_token'])) {
	$access_token = $json['access_token']; // your access token
