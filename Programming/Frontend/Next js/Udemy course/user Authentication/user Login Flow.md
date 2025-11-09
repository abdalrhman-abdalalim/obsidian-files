### **User Login Flow**

1. **Client Sends Credentials:**
    
    - The user enters their **username** and **password** into the login form.
        
    - The client (e.g., a web browser or mobile app) sends these credentials to the server, typically using a secure HTTPS connection to prevent eavesdropping.
        
2. **Server Verifies Credentials:**
    
    - The server checks the provided credentials against its database.
        
    - If the credentials are correct, the server proceeds to the next step.
        
    - If the credentials are incorrect, the server responds with an **authentication error**.
        
3. **Create and Store User Session:**
    
    - If the credentials are valid, the server creates a **session** to keep track of the authenticated user.
        
    - This session can be stored in memory, a database, or a session management system like Redis.
        
4. **Send Cookie with Session ID:**
    
    - The server sends a **cookie** containing the **session ID** back to the client.
        
    - This cookie is usually **HTTP-only** and **Secure** to protect it from cross-site scripting (XSS) attacks.
        
5. **Client Stores the Cookie:**
    
    - The client stores the cookie and automatically includes it in future requests to the server, allowing the server to identify the authenticated user.
        
6. **Authenticated User Access:**
    
    - With the valid session cookie, the user can access protected routes and resources on the server until the session expires or the user logs out.