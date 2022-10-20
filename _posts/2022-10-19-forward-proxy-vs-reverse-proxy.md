---
title: Forward Proxy VS Reverse Proxy
date: 2022-10-19 18:00:00 +0800
categories: [Blogging, Technology, Software Development]
tags: [network, proxy]
---

> **Proxy server** act as a mediary between client device and a web server (user's destination). The existent of proxy is to make sure the related party is safe in terms of  its privacy and security. Thus, proxy server implementation is necessary nowadays to negate the risk data leaks and personal information breaches.

## Proxy

- In networking field, proxy server is a mediary party between the client (user) and the web server (user's destination).
- Proxy server act as a 'middle-man' that will relay user's request and pass it to the targeted server, proxy server will also send the server's response back to user.

## Forward Proxy

- The term 'proxy', 'proxy server' or 'web proxy' are usually refers to **forward proxy**. Forward proxy is the most commonly use by both small and big companies.
- Act as a gatekeeper for the user or the client (places in front of the client) and ensures that no web server (destination) communicates directly with the client

### Why Forward Proxy

- To bypass organization browsing restriction.
- To prevent user from accessing certain website.
- To protect privacy and security from being breach.
- To filter content on the internet.
- To ensure client's anonymity.

## Reverse Proxy

- No use for regular user, but crucially needed by the services provider and websites that has tons of visitor daily.
- Act as a gatekeeper for the backend server (destination) (places in front of the server) and ensure that no user communicates directly with the server

### Why Reverse Proxy

- Load balancing - To balance traffic and request loads
- To ensure server's anonymity.
- Caching commonly requested data to boost speed - Image CDN, CDN
- To establish security and prevent unwanted access from suspicious IP addresses.

Below shows the representation of forward and reverse proxy:
![image of forward proxy VS Reverse proxy](/posts/20221019/forward-proxy-vs-reverse-proxy.png)
*Source: [Forward proxy VS Reverse proxy - kinsta.com](https://kinsta.com/blog/reverse-proxy/)*

---

## Sources

1. [Cloudflare - What is reverse proxy?](https://www.cloudflare.com/learning/cdn/glossary/reverse-proxy/)
2. [ScrapingAnt - Reverse proxy vs forward proxy](https://scrapingant.com/blog/reverse-proxy-vs-forward-proxy)
3. [Oxylabs - Reverse proxy vs forward proxy](https://oxylabs.io/blog/reverse-proxy-vs-forward-proxy)
