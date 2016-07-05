###### Sample Code for generating JWT token

```java
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.impl.crypto.MacProvider;
import java.security.Key;

// 1. Create the JSON string with user properties.
String payload = "{\"uuid\": \"1234567890\",\"first_name\": \"John\",\"last_name\" : \"Doe\",\"phone\" : \"+111111111\",\"email\" : \"john@email.com\",\"admin\": true}";

// 2. Choose the encoding algorith 'HS256'
Map<String, Object> header = new HashMap<>();
header.put("alg", "HS256");
header.put("typ", "JWT");

// 3. Use your secret key provided by Avaamo here.
byte[] apiKeySecretBytes = "<YOUR SECRET KEY>".getBytes();
Key signingKey = new SecretKeySpec(apiKeySecretBytes, SignatureAlgorithm.HS256.getJcaName());

String jwtToken = Jwts.builder().setPayload(payload).signWith(signingKey).setHeaderParams(header).compact();

```

```xml
<!-- JWT Library to use -->
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.6.0</version>
</dependency>

<!-- Library Dependencies -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.7.5</version>
</dependency>

<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-annotations</artifactId>
  <version>2.7.5</version>
</dependency>

```

