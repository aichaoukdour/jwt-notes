# 🌐 Complete Guide to JSON Web Tokens (JWT)
> **A powerful tool for secure data transmission between entities.**  
> This guide covers all the key aspects of understanding and using JSON Web Tokens (JWT) effectively.

<img width="222" alt="Screenshot 2025-01-17 091122" src="https://github.com/user-attachments/assets/6c9b58c4-7890-4367-a074-21f406e5bb78" />

---

##  Introduction  
A **JSON Web Token (JWT)**, pronounced *“jot”*, is an open standard ([RFC 7519](https://www.rfc-editor.org/rfc/rfc7519)) used to transmit information between entities as a JSON object that is signed.  
### 📌 Key Points:
- **Secure**: Digitally signed with secret keys or public/private keys (RSA, ECDSA).  
- **Compact**: Easily transmitted via HTTP/HTML.  
- **Not Encrypted**: The information is not hidden; avoid storing sensitive data.

---

##  Why Use JWTs?  

###  Problem: Stateless nature of HTTP  
HTTP is a stateless protocol that means a new request does not remember anything about the previous one. So for each request, you need to login and authenticate yourself (figure ). Now, this sounds like a lot of work.

<img width="473" alt="Screenshot 2025-01-17 092952" src="https://github.com/user-attachments/assets/cd88782e-861e-4416-bb03-e7f52e05dff8" />

### Traditional Solution: Server-side Sessions  
So, the solution to deal with this is the use of what’s called a session. A session is an object stored on the server that helps the user to stay logged in or to save any reference to their account. Figure 2 shows the overall flow of this process.

<img width="517" alt="Screenshot 2025-01-17 093303" src="https://github.com/user-attachments/assets/313506a2-846c-4da1-b8bf-d907a754464b" />

First, the user submits a username and a password that are authenticated by the server. If the authentication is successful a session ID is generated for the respective client. The generated session ID is returned to the client and is stored on the server-side as well.
Now, the client just needs to send its session ID along with the request to authenticate itself and retrieve necessary information. The server will then check if the session ID is valid or not. If the session is still valid, it will respond with the requested webpage/data. And if not, the server will respond with an error message stating that the request made is unauthorized.

. Limitations:  
   - 📉 **Scalability**: Sessions stored on the server.  
   - ⚙️ **Session Management**: Complexity in handling expired/inactive sessions.  
   - 🕒 **Performance**: Constant checks in memory or databases.

---

### The better and effective solution
The JSON Web Token (JWT) does not use sessions and hence prevents the above problems. When you send your credentials to the server instead of making a session, the server will return a JSON Web Token. You can use that JWT to do whatever you want with the server (Of course, the things that you are authorized to do).
Consider a JWT like a hotel key: When you enter the hotel, first you need to register yourself at the reception to receive your key card. You can use that key card to open and close your room, access common amenities like Bar, Fitness Centre, etc. But you cannot use that key card to access someone else’s room or Manager’s office since you are not authorized to do so. The key card comes with an expiration date, and it becomes useless once your stay has ended at the hotel.
Similarly, you can use your JWT token generated from one server to access resources on different servers. The JWT token contains claims like expiration date/time that can be used to check its validity..

---

### ✅ JWT Advantage  
- No need for server-side session management.  
- Can act as a universal key (like a hotel card).

---

##  Structure d’un JWT  
Un JWT est une chaîne encodée composée de trois parties séparées par des points (`.`) :
![JWT](https://github.com/user-attachments/assets/46575af0-8ee3-4fb3-ae05-f02400f2cce2)

### 1️⃣ **Header** 
The header consists of two parts i.e. the type of token and the algorithm used for signing (such as HMAC SHA256 or RSA). The token type helps to interpret the token and in this case it’s JWT
Exemple :  
```json
{
  "typ": "JWT",
  "alg": "HS256"
}

```
### 2️⃣ **Payload**
The payload consists of the session data called as claims. Claims provide information about the client/user. There are three types of claims: registered, public, and private claims.

#### Registered Claims: 
These type of claims are predefined claims which can be used for increasing the security. These claims are not mandatory but recommended. Some of these claims are:
iss (Issuer) Claim: The “iss” claim helps to identify the issuer of the token.
sub (Subject) Claim: The “sub” claim identifies the subject of the JWT.
aud (Audience) Claim: The “aud” claim identifies the recipients that the JWT is intended for.
exp (Expiration Time) Claim: The “exp” claim is used to identify the expiration time on or after which the JWT must not be valid. Its value must be a number containing a NumericDate value. One important thing is that the current date/time must be before the expiration date/time.
nbf (Not Before) Claim: The “nbf” claim identifies the time before which the JWT must not be accepted for processing. The current date/time must be after or equal to the not-before date/time
iat (Issued At) Claim: The “iat” claim is used to identify the the time at which the JWT was issued. This claim can be used to determine the age of the JWT.
jti (JWT ID) Claim: The “jti” claim gives a unique identifier for the JWT. The “jti” value is a case-sensitive string and it should be assigned in such a manner that ensures that there is a negligible probability that the same value will be repeated. The “jti” claim can be used to prevent the JWT from being replayed.

#### Public Claims: 
These type of claims can be defined by group of people using the JWTs. Whenever any new claim name is defined it is necessary that it should be registered in the IANA “JSON Web Token Registry” or it should contain a collision resistant name to avoid collisions.

#### Private Claims: 
These are custom claims defined and created by two parties in order to exchange information between them.
### 3️⃣ **Signature**
Signature is the most important part of JWT which helps to verify if the information within the token has been tampered with or not. It can be also used to verify that the sender of the JWT is who it says it is.
In order to calculate the signature, you require three things: an encoded header, an encoded payload, and a secret. First, you will take the encoded header and encoded payload and concatenate them with a period separator to form a string. This concatenated string will be hashed using an algorithm specified in the header and a secret key to calculate the signature.

---

## ⚙️ How JWT Works ?
![JWT (1)](https://github.com/user-attachments/assets/ddac4b81-9b38-4d80-ae38-4885e1c64497)

A JSON Web Token (JWT) works as a secure way to authenticate and authorize users in a stateless manner. 
When a user logs in by submitting their credentials (like a username and password), the server authenticates the user. Upon successful authentication, the server generates a JWT, which is sent back to the client. 
The client stores this token and uses it to request access to protected resources by including the JWT in the Authorization header, following the Bearer schema. When the server receives a request, it checks the Authorization header for the JWT, validates it using a secret key, and grants access if the token is valid. 
The JWT contains embedded information about the user, such as their ID and privileges, allowing the server to identify and authorize the user without needing to query the database repeatedly. 
This also enhances security since the token is signed with a secret key that only the server knows, making it impossible for attackers to alter the token without invalidating it. 
This mechanism ensures that only authorized users can access protected resources, and any tampering attempts are immediately detected by the server.

--- 
## Advantages of JSON Web Token

#### Compactness: 
JSON is less verbose than XML and therefore when it is encoded it takes up less space making JWT more compact then SAML.
No need of Session: The JWT can contain all the necessary information about the user and therefore there is no need to maintain a session object on the server, saving up server memory.
#### Built-in Expiration: 
The JWT has claims that can be used to assign it a expiration date/time. Therefore, the token can become invalid on its own after the expiration period.
No need of Cookies: The token can be stored in the localStorage, indexDB, or some native store. This will provide a protection against CORS and CSRF attacks.
#### Compatibility:
In most programming languages, JSON parsers are popular because they map directly to objects. Contrary, there is no natural document-to-object mapping in XML. This makes it simpler than SAML assertions to operate with JWT.

That’s it! Now you know pretty much everything about JSON Web Token.

---

## 📥 Installation
1. Install JWT Library
To start using JWT in your project, you need to install the necessary libraries for your environment.

Node.js (for a JavaScript/Node backend)
For Node.js, you can use the jsonwebtoken package:

```
npm install jsonwebtoken
```
Spring Boot (for Java backend)
For Java projects using Spring Boot, you can add the following dependency to your pom.xml:
```
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt</artifactId>
    <version>0.11.5</version>
</dependency>
```
Python (for Python backend)
In Python, you can use the pyjwt package:
```
pip install pyjwt
```
---
## 📖 References
Here are some helpful resources to further your understanding of JWT and its implementation.

### 📖 Official Documentation
1. [JWT Official RFC 7519 Specification](https://www.rfc-editor.org/rfc/rfc7519)  
   The official specification of JSON Web Token (JWT) by the IETF.

2. [JWT.io Introduction](https://jwt.io/introduction/)  
   A comprehensive guide and tutorial on using JWTs with various programming languages.

### 🧑‍💻 Tools and Libraries
- **[JWT.io Debugger](https://jwt.io/#debugger-io)**  
  A tool to decode, verify, and generate JWTs directly in your browser.
- **[jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)**  
  A popular Node.js library for working with JWTs.
- **[pyjwt](https://pypi.org/project/PyJWT/)**  
  Python library for encoding and decoding JSON Web Tokens (JWT).



