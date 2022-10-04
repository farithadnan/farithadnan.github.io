---
title: API Gateway
date: 2022-10-04 15:59:00 +0800
categories: [Blogging, Developer]
tags: [programming, networking, api]
---

## Definition
- **API Gateway** is a software that handles all the API Calls from different environment into one place. 
- It will take request from user and route it to the backend services, gather appropriate data based on a request then send it back to the requestor in a single package. 
- Handle all user request and execution. 
- API Gateway usually used in application that uses Microservice Architecture. Which mean it's scalable, independent and flexible to upgrade and changes.


## How it works?
1. **Request Routing** - Receive API request, turns it into multiple requests to check a routing map that determine where each request should be sent before send the request to the right microservice.
   
2. **API composition** - Provides ability to arrange workflow as the requested information from multiple microservices is being combine together before sending the data bundle to the requestor.
   
3. **Protocol translation** - The gateway translate API Protocol from what devices did the end user uses. whether it's web browser or mobile. Then, the gateway will transform and send the data back to the requestor in the way they can view based on its device's API Protocol.

### Example: 
> - Web Browser - Can see all the information.
> - Mobile - Can see limited number of information.
{: .prompt-info }


## Benefits 
- **Microservice Security** - API Gateway act as a shield for the application's backend, meaning the application endpoints is not being exposed. Plus with the usage of HTTPS or HTTP with SSL encryption it will also increase its security and performance. 

- **API authentication** - By the usage of authenticating API calls and authorization it can protects against mistakes and data breaches. Authorization and authentication can also include virus scanning and other security functions.
  
- **Input validation** - Ensure all the API request has all the correct  information before sending it to the microservice. 
  
- **Faster Response Times** - Send request right services, thus reducing traffic and latency when processing the information.
  
- **Microservice Load Balancing** - API Gateway always keeps track of request that being send to different microservices. It will balances the load between the nodes to increase efficiency and make sure the application is always okay.

- **Rate Limiting** - API Gateway monitors traffic coming from all sources and make sure the system is not flooded with request by limiting API request from the clients. 

---
# Sources:
1. [What is API gateway? - IBM](https://www.ibm.com/cloud/blog/api-gateway)