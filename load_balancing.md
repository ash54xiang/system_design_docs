# Load Balancing Overview

##  Concept
* A load balancer is a device that acts as a reverse proxy and distributes network or application traffic across a number of services.
* it helps scale horizontally across an ever-increasing number of servers


## How does the Load Balancer work?
* Define IP or DNS name for LB
  * define one IP address and/or DNS name for a given application, task or website, to which all requests will come. This IP address or DNS name is the LB server.
* Add backend pool for LB
  * can be access internally **ONLY**
* Deploy LB
  * deployed as:
    * Proxy - sits between app servers and users worldwide and accepts all traffic
    * Gatewy - assgins a user to a server once and leaves the interaction alone thereafter
* Redirect requests
  * when LB system is in place, all requests to the app come to the LB are redirected according to algorithms implemented.


## Types of LBs
* "Layer 7 LB"
* "Layer 4 LB"

## LB Locations
* Between user and web servers (User => Web Servers)
* Between web servers and an internal platform layer (application servers, cache servers) (Webservers => App or Cache servers)
* Between internal platform layer and database (App or Cache servers => Database servers)

## Algorithms
* Least connection
* Least response time
* Lease bandwidth
* Round robin
* Weighted round-robin
* IP Hash

## Reference
* https://www.thegeekstuff.com/2016/01/load-balancer-intro/