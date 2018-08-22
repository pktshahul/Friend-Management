# Friend-Management
Friend Management

# friend-management-service
API server that does simple "Friend Management"   


### Build and run project

``` 
mvn clean install
java -jar target/friend-management-service-1.0-SNAPSHOT.jar

```

###  Docker   

```
docker run -p 5000:8080 shahulimg/friend-management-service:1.0-SNAPSHOT
```

### Databse   

Application is using H2 database

```
http://host:8080/h2  


###   Error format   

```  
{
  "status": "BAD_REQUEST",
  "timestamp": "27-06-2018 11:19:30",
  "message": "validation failed",
  "errorCode": 0,
  "errors": [
    "Friend list should contain exactly 2 emails",
    "Invalid email ids"
  ]
}
```

###   Error Codes and messages

```
2001 - "Email address is already registered"
2002 - "Email address is not registered"
3001 - "Email addresses are already connected as friends"
3002 - "Email addresses are not connected as friends"
3003 - "One email have blocked another email's updates"
4001 - "Already subscribed for updates"
5001 - "Already unsubscribed from further updates"
```



# User Stories
# 0. User can register email id using 
URL - http://localhost:8080/api/email/register
Methos - POST
Request Format
```
{
  "email": "john@example.com"
}
```
Response Format
```
{
  "success":true
}
```
Error codes  

2001	- Email address is already registered

# 1. As a user, I need an API to create a friend connection between two email addresses.
After successfully adding friend . 
Both email ids will automatically subscribe for updates from each other
URL - http://localhost:8080/api/friend/add
Methos - POST
Request Format
```
{
  friends:
    [
      "andy@example.com",
      "john@example.com"
    ]
}
```
Response Format
```
{
  "success":true
}
``` 
  
  
Error codes   

2002  - Email address is not registered  
3001  - Email addresses are already connected as friends  
3003  - One email have blocked another email's updates

# 2. As a user, I need an API to retrieve the friends list for an email address. 
URL - http://localhost:8080/api/friend/all 
Methos - POST
Request Format
```
{
   "email":"andy@example.com"
}
```
Response Format
```
{
    "emails": [
        "john@example.com"        
    ],
    "success": true,
    "count": 1
}
```  

Error codes  

2002	- Email address is not registered

# 3. As a user, I need an API to retrieve the common friends list between two email addresses.
URL - http://localhost:8080/api/friend/common
Methos - POST
Request Format
```
{
  "friends":
    [
      "andy@example.com",
      "john@example.com"
    ]
}
```
Response Format
```
{
    "emails": [
        "common@example.com"
    ],
    "success": true,
    "count": 1
}
```
Error codes   

2002	- Email address is not registered  

# 4. As a user, I need an API to subscribe to updates from an email address. 
URL - http://localhost:8080/api/notifications/subscribe .  
Methos - POST  
Request Format
```
Request : 
{
  "requestor": "lisa@example.com",
  "target": "john@example.com"
}
```
Response Format
```
{
  "success": true
}
```
Error codes   

2002	- Email address is not registered     
4001	- Already subscribed for updates    

# 5. As a user, I need an API to block updates from an email address. 
URL -  http://localhost:8080/api/notifications/unsubscribe
Methos - POST
Request Format
```
{
  "requestor": "andy@example.com",
  "target": "john@example.com"
}
```
Response Format
```
{
  "success": true
}
```
Error codes   

2002	- Email address is not registered     
5001	- Already unsubscribed from further updates        

# 6. As a user, I need an API to retrieve all email addresses that can receive updates from an email address.
URL - http://localhost:8080/api/message/send
Methos - POST
Request Format
```
{
  "sender":  "john@example.com",
  "text": "Hello World! kate@example.com"
}
```
Response Format
```
{
    "success": true,
    "recipients": [
        "lisa@example.com",
        "kate@example.com"
    ]
}
```
Error codes   

2002	- Email address is not registered     

