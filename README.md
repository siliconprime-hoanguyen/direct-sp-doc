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

### protected api must be called with header

```javascript
{
	Authorization: Bearer xxxxxxx //xxxxxxx is the token received when calling login api successfully.
}
```

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
	"uid":"ab@c.com"
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

* **get account by account id (protected)**
```javascript
get /accounts/:accountId 
```
* **update account by account id (protected)**
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

* **change password (protected)**
```javascript
put /accounts/:accountId/password
```
```javascript
{
  "currentPassword":"xxxx",
  "newPassword": "xxxxx"
}
```

* **set online (protected)**
```javascript
post /accounts/:accountId/setonline
```

* **set offline (protected)**
```javascript
post /accounts/:accountId/setoffline
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

* **save chat message**
```javascript
post /messages
```
```javascript
{
   sender: 'abc', //optional
   recipient: 'def', //optional
   data:{
   	streamId: '123' //optional
	//can put any field here.
   }
}
```
* **get chat message by streamid, descending sort by createdAt by default**
```javascript
get /messages/list/getByStreamId/:streamId
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
* **cancel streaming request** 
```javascript
post /streams/cancel/:streamId
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
get streams/list/get?skip=0&limit=123&status=missed,requested,streaming
```

* **get active call list by accountid** 
```javascript
get streams/list/getactive?skip=0&limit=123
```

* **get incoming call list by accountid** 
```javascript
get streams/list/getincoming?skip=0&limit=123
```

* **get missed call list by accountid** 
```javascript
get streams/list/getmissed?skip=0&limit=123
```
* **get on going call list by accountid** 
```javascript
get streams/list/getongoing?skip=0&limit=123
```

* **get call history** 
```javascript
get streams/list/gethistory?skip=0&limit=123
```

* **get stream by stream id** 
```javascript
get streams/:streamId
```


