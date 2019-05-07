#### Description
**sinaweibopy3** plays a role in the use of **sinaweibo API** just as what Twurl does in the use of Twitter API. It asks for the authorization of a specified user to get the access token for the client application, and then signs all requests with that access token.

Specifically, **sinaweibopy3 is for python3 version**. If you're using python 2, please click here: [sinaweibopy](https://github.com/michaelliao/sinaweibopy)
#### Getting Started
If you start to use sinaweibo API from scratch, the first thing is to apply for a developer account to access sinaweibo API:

https://open.weibo.com/wiki/API

After you have that access you can create a new app and generate a App Key and App Secret.

When you have your App Key and Secret you authorize your sinaweibo account to make API requests with your App Key and Secret. This will return an URL that you should open up in your browser. Authenticate to sinaweibo, and then enter the returned token **code** back into the terminal. Assuming all that works well, you will be authorized to make requests with the API. Sounds complicated? Don't worry, `sinaweibopy3` will do the work for you.
#### Usage
1. Import `sinaweibopy3` in your file
```
import webbrowser
import sinaweibopy3
```
2. Set some parameters of your application: APP_KEY, APP_SECRET, REDIRECT_URL

3. Use `sinaweibopy3` to get the access token for the application.
```
client = sinaweibopy3.APIClient(app_key=APP_KEY, app_secret=APP_SECRET, redirect_uri=REDIRECT_URL)
url = client.get_authorize_url()
webbrowser.open_new(url)
result = client.request_access_token(input("please input code : "))
client.set_access_token(result.access_token, result.expires_in)
```

4. Make requests with API using the access token.

  **Example**: To get some of the latest public microblogs and the user information:                
  `print(client.public_timeline())`

  The data is in json. you can further parse it and extract the information you need.

#### What should I do if I want to get other kinds of data from sinaweibo API?

1. Look up the required url and parameters of the data on https://open.weibo.com/wiki/API
![url](https://github.com/Juliecodestack/sinaweibopy3/blob/master/url.png)
![parameters](https://github.com/Juliecodestack/sinaweibopy3/blob/master/parameters.png)
2. In `sinaweibopy3.py`, add a function.
```
def funtion_name(self):
  result = _http_get('%s'% (self.api_url)  + 'the remaining part of url after extracting https://api.weibo.com/2 ',
             other requirement parameters, such as:
             access_token=self.access_token,
             ...
              )
      return result  
```
3. Call the fuction in your file by:
`result=client.funtion_name()`

  If the fuction works well, you'll get the required data. Good Luck!
