## server
- intial dev: http://directapi.codehub.io

## apis

### registration & authentication

#### registration
##### post /auth/register
```javascript
{
  "email":"codehubio@gmail.com",
  "password":"12345678", // must be more than 6
  "fullName":"hoanguyen"

}
```
#### activate
##### post /auth/activate
```javascript
{
	"token":"12345678"
}
```

#### login
##### post /auth/login
```javascript
{
	"password":"12345678",
	"email":"ab@c.com"
}
```
### account service

#### get account by account id

#####
##### get /accounts/:accountId 
