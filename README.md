## server
- intial dev: http://directapi.codehub.io

## apis

### registration & authentication

* **registration**
```javascript
post /auth/register
```
```javascript
{
  "email":"codehubio@gmail.com",
  "password":"12345678", // must be more than 6
  "fullName":"hoanguyen"

}
```
* **activate**
```javascript
post /auth/activate
````

```javascript
{
	"token":"12345678"
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
