## Practical 6 : Securing Redis and MongoDB (Authentication, Encryption, RBAC, and Security Audit)

```
AIM

The aim of the practical is to verify authentication, encryption and role based access control for redis and mongoDB. It is also for the basic security audit of the configured database.
```
```
OBJECTIVE

1. Enable password-based authentication and Access Control Lists (ACL) in Redis.
2. Enable TLS encryption for Redis connections (at least at the configuration and client-connection level).
3. Enable authentication and RBAC in MongoDB using built-in user roles and custom roles.
4. Enable TLS for MongoDB so that all traffic is encrypted in transit.
5. Execute a simple security audit checklist (tests and commands) for both databases and record findings.
```
```
THEORY

1. Authentication in both redis and mongodb is the security layer that verifies the identity of a client before allowing them to access the database. However in mongodb the authentication is tied to role base access control where if the user prove who it is, mongodb checks what the user is allowed to do. But in redis it is for speed the authentication is simple than the mongdb. Redis uses the ACL ( Access control list), lagacy password and speed warning. 

2. Encryption in redis and mongodb is securing the data at different stages including data at transit and at the rest. However in mongodb the data is encrypted in the persistent layer and redis it stores the data in RAM for faster retrival the data is encrypted on the RAM. 

3. Role base access control in redis and mongodb refers to the security mechanism used to manage permissions based on user roles rather individual user accounts. However mongodb prodives a robust RBAC for the database that supports built in roles and customized roles. In redis the RBAC is supported by Access control List ( ACL ) which is implemented to define command level permissions.
```
Enabling ACL and created users in redis.conf

![alt text](Assets/ACL.png)

Testing as admin 
![alt text](Assets/admin.png)

Test as app_user (RBAC check)

![alt text](Assets/user.png)

all the above demonstrates RBAC using ACL rules. 

Enabling TLS for Redis

1. Generate Self-Signed Certificates
- Created a CA ( Certificate Authority ) for this lap.
- Created a private key where only I can sign with it.

![alt text](Assets/TLS.png)

This creates ca.crt, redis.crt, redis.key in /etc/redis/tls.

2. Update redis.conf for TLSRBAC i

![alt text](Assets/TLS.png)


## Part B : Securing MongoDB 

- Start MongoDB Without Auth (Initial Setup Only). MongoDB without auth fails to load. 
  
![alt text](Assets/mongodbadmin.png)

- Enable Authentication in mongod.conf which turns on  turns on access control (RBAC)
![alt text](Assets/mongonano.png)

- Testing Authentication.
![alt text](Assets/mongoauth.png)

The output shows the authenticated user and roles, confirming that auth is working.

- When connecting without username and password the show dbs command is failing. 

![alt text](Assets/show.png)

## Create Application Database, Role, and User (RBAC)

- creating an application specific database and limit permissions using roles. For this I logged in a mongosh, authenticated as rootAdmin. Created limited role for application users and created an application user with appuser. 
  
![alt text](Assets/rootadmin.png)

- Logged in as app user and inserted a data in myapp.
![alt text](Assets/app-user.png)

- Now when trying to find user logged in as app user it fails, since the app user does not have the permission on the admin database. This proves the RBAC where app user has limitted rights on the myapp.customers. 
  
![alt text](Assets/userfail.png)

## Enable TLS Encryption for MongoDB

- TLS is used in data transit to enclrypt the data. 
- Generating a self-signed certificates for testing the TLS with MongoDB.
  
![alt text](Assets/tls.png)

- Updating the mongod.conf for TLS and now all the connections in MongoDB must use the --tls flags.

![alt text](Assets/conf.png)

- Connecting with TLS and Auth, here the command fails without --tls and without correct credentials the authentication fails. This shows how encryption and RBAC are enforced.

![alt text](Assets/tlsauth.png)

