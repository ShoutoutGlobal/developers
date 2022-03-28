# Developers Documentation

Our API allows you to retrieve informations from our website via GET request and supports the following query parameters:

| Name  | Meaning | Values | Description | Required |
| ------------- | ------------- | 
| type  | Query type.  | get_user_data, posts_data | This parameter specify the type of the query. | YES |
| limit  |Limit of items.  | LIMIT | This parameter specify the limit of items. Max: 100/Default:20 | YES |

# How to start?

 Markup : - Create a development application.
          - Once you have created the app, you'll get APP_ID, and APP_SECRET.
          
Markup :         ![picture](https://www.shoutout.ga/themes/maindesign/img/developer.png)

Markup : - To start the Oauth process,use the link https://www.shoutout.ga/oauth?app_id={YOUR_APP_ID}
         -  Once the end user clicks this link, he/she will be redirected to the authorization page.
         - Once the end user authorization the app, he/she will be redirected to your domain name with a GET parameter "code", example: http://yourdomain/?code=XXX
         - In your code, to retrieve the authorized user info, you need to generate an access code, please use the code below:
PHP:
Markup : <kbd><?php
	$app_id = 'YOUR_APP_ID'; // your application app id
	$app_secret = 'YOUR_APP_SECRET'; your application app secret
	$code = $_GET['code']; // the GET parameter you got in the callback: http://yourdomain/?code=XXX

	$get = file_get_contents("https://www.shoutout.ga/authorize?app_id={$app_id}&app_secret={$app_secret}&code={$code}");

	$json = json_decode($get, true);
	if (!empty($json['access_token'])) {
		$access_token = $json['access_token']; // your access token
	}
?></hbd>

Markup : - Once you got the access code, simple call the data you would like to retrieve, Example:
PHP:
Markup : <hbd>if (!empty($json['access_token'])) {
	$access_token = $json['access_token']; // your access token
	$type = "get_user_data"; // or posts_data
	$get = file_get_contents("https://www.shoutout.ga/app_api?access_token={$access_token}&type={$type}");
}</hbd>
Respond:
Markup : <hbd>Jsonoutput
{
	"api_status": "success",
	"api_version": "1.3",
	"user_data": {
		"id": "",
		"username": "",
		"first_name": "",
		"last_name": "",
		"gender": "",
		"birthday": "",
		"about": "",
		"website": "",
		"facebook": "",
		"twitter": "",
		"vk": "",
		"google+": "",
		"profile_picture": "",
		"cover_picture": "",
		"verified": "",
		"url": ""
	}
}</hbd> 
