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

## 🤔 Pourquoi utiliser un JWT ?
###  Problème : La nature sans état du protocole HTTP  
Chaque requête HTTP est indépendante. Cela oblige à s’authentifier à chaque requête.  

###  Solution traditionnelle : Sessions côté serveur  
1. Création d’un **ID de session** après authentification.  
2. L’ID est stocké côté serveur et envoyé avec chaque requête.  
3. Limites :  
   - 📉 **Évolutivité** : Sessions stockées sur le serveur.  
   - ⚙️ **Gestion des sessions** : Complexité accrue pour gérer les sessions expirées/inactives.  
   - 🕒 **Performances** : Vérifications constantes en mémoire ou en base de données.

### ✅ Avantage JWT  
- Aucune gestion des sessions côté serveur.  
- Utilisable comme clé universelle (comme une carte d’hôtel).

---

##  Structure d’un JWT  
Un JWT est une chaîne encodée composée de trois parties séparées par des points (`.`) :
![JWT](https://github.com/user-attachments/assets/46575af0-8ee3-4fb3-ae05-f02400f2cce2)
