# Client Registration

To access SmartHive resources by using SmartHive APIs, first register your application with SmartHive. You can register your application as one of the following client types:

- Server-based application
- Client-based application
- Self client

After you register your application, you receive a client ID and client secret. Use them to get the access token that you need to make API calls to SmartHive.

## To register your application

1. Go to the SmartHive API console, then select **GET STARTED**.

2. Point to your application’s client type, and then select CREATE NOW. If you previously added an application, select **ADD CLIENT** in the upper-right corner.

3. Enter the required details, and then select **CREATE**. The required details vary by client type.

| Details required | Server-based | Client-based | Self client |
| :---        | :----  |      :---- | :---- |
| Client Name    | Y    | Y  | Y|
| Homepage URL   | Y       | Y  | N |
| Authorized Redirect URI  | Y       | Y   | N |
| Javascript Domain  | N       | Y   | N |


**INFO:**

| Label | Description |
| :---        | :----  |
| Homepage URL    | The full URL of your application’s home page.| 
| Authorized Redirect URI       | The URI of the application that the authorization server (SmartHive Accounts) sends the response to. The response includes the authorization code, or the access token for a client-based application, after the user grants consent. The URI must begin with https:// or http://. To add more redirect URIs, select [plus]. Example: https://www.panacim.com/oauthredirect  |
| JavaScript Domain       | If your application is a client-based JavaScript application, specify its JavaScript domain. The domain must begin with https:// or http://. To add more JavaScript domains, select [plus].  |


You can find the client ID and client secret on the Client Secret tab of your application in the console.

To learn more about self clients, see Self client.