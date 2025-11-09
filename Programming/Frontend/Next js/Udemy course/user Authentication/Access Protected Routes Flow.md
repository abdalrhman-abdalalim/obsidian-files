### **Accessing Protected Routes Flow**

1. **Client Requests Protected Routes:**
    
    - The client (e.g., web browser or mobile app) makes a request to access a protected resource, such as a user profile, settings, or dashboard.
        
2. **Server Checks Session Cookie Validity:**
    
    - The server receives the request and checks for the presence of a **session cookie** (usually with the session ID).
        
    - The server verifies whether the session ID in the cookie corresponds to a valid and **active session** stored on the server.
        
3. **Valid Session - Server Returns Resources:**
    
    - If the session is valid and active, the server retrieves the requested resources (e.g., user data, profile, etc.) and sends them back to the client.
        
4. **Invalid or Expired Session - Not Authenticated:**
    
    - If the session is **invalid**, **expired**, or **missing**, the server responds with an **authentication error**, denying access to the protected resources.
        
    - The client may be redirected to the login page to re-authenticate.