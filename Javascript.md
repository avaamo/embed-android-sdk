###### Sample Code for generating JWT token

```html
// JS library to use
<script language="JavaScript"
  type="text/javascript" src="http://kjur.github.io/jsrsasign/jsrsasign-latest-all-min.js">
</script>
```

```javascript
var payload = {
  "uuid": "1234567890",
  "first_name": "John",
  "last_name" : "Doe",
  "phone" : "111111111",
  "email" : "john@email.com",
  "admin": true
}

var header = {
  "alg": "HS256",
  "typ": "JWT"
};

var secretKey = 'abcd'

var token =
    KJUR.jws.JWS.sign("HS256",
        JSON.stringify(header),
        JSON.stringify(payload),
        {rstr: secretKey});
```
