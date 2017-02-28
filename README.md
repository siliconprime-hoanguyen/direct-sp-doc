## server
- intial dev: http://directapi.codehub.io

## test result
```javascript
http://test.codehub.io/index.html
```

## installation

* for each module, e.g, authentication, please navigate into and type **npm install**.
* config files are located at root folder and in service folders respectively, fields should be descriptive themselves.
* modify port numbers in **start.sh** and config files for services
* run **start.sh**

## tests

```javascript
npm test
```

## apis

### registration & authentication

* **registration**
```javascript
post /accounts
```
```javascript
{
  "email":"codehubio@gmail.com",
  "password":"12345678", // must be more than 6
  "fullName":"hoanguyen",
  "phone": "123123",
  "countryCode":"+84"
}
```
* **activate**
```javascript
post /accounts/activate/tokens
````

```javascript
{
	"token":"12345678"
}
```
* **resend activate email**
```javascript
post /accounts/activate/sendemail
````

```javascript
{
	"email":"ancsd@fdsfds.com"
}
```

* **login**

```javascript
post /auth/login
```

```javascript
{
	"password":"12345678",
	"email":"ab@c.com"
}
```
* **sending email to reset password**

```javascript
post /auth/forgotpassword
```

```javascript
{
	"email":"ab@c.com"
}
```
* **reset password with sent token**

```javascript
post /auth/resetpassword
```

```javascript
{
	"token":"xxx",
	"newPassword":"12321321" //must be more than 6
}
```

### account service

* **get account by account id**
```javascript
get /accounts/:accountId 
```
* **update account by account id**
```javascript
post /accounts/:accountId 
```
```javascript
{
  "fullName":"hoanguyen",
  "status": "active", // ['active', 'inactive', 'banned']
  "userStatus": "online", // ['online', 'offline']
}
```
```javascript
this api is for update general info of account so important fields like email, password, id will be **ignored**. to change those fields, please call other specific apis
```

* **change password**
```javascript
put /accounts/:accountId/password
```
```javascript
{
  "currentPassword":"xxxx",
  "newPassword": "xxxxx"
}
```


### admin service

* **ban account account id**
```javascript
post /admin/accounts/ban/:accountId 
```


### notification service

* **add device**
```javascript
post /notifications/addDevice
```
```javascript
{
   accountId: 'xxxx',
   deviceBundleId: 'com.siliconprime.direct',
   deviceMode: 2,  //1 for sandbox, 2 for production
   deviceToken: 'xxxx',
   type: 'pn' // pn: normal push notification, 'voip': reserve for callkit, default is 'pn'
   deviceType: 'ios' //or android
}
```

### stream service

* **request streaming by email**
```javascript
post /streams/request
```
```javascript
{
"email" :"codehubio@gmail.com"
}
```
* **accept streaming request**
```javascript
post /streams/accept/:streamId
```
* **start streaming request**
```javascript
post /streams/start/:streamId
```
* **stop streaming request**
```javascript
post /streams/stop/:streamId
```
* **authentication pusher channel** (called by the SDK)
```javascript
post /notifications/socket/authenticatepusherchannel
```

* **get call list by accountid** 
```javascript
get streams/getbyaccountid/:accountId?skip=0&limit=123&status=missed,requested,streaming
```

* **get active call list by accountid** 
```javascript
get streams/getactivebyaccountid/:accountId?skip=0&limit=123
```

* **get incoming call list by accountid** 
```javascript
get streams/getincomingbyaccountid/:accountId?skip=0&limit=123
```

* **get missed call list by accountid** 
```javascript
get streams/getmissedbyaccountid/:accountId?skip=0&limit=123
```
* **get on going call list by accountid** 
```javascript
get streams/getongoingbyaccountid/:accountId?skip=0&limit=123
```

* **get call history** 
```javascript
get streams/gethistory/:accountId?skip=0&limit=123
```


