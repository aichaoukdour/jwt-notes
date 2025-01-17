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
