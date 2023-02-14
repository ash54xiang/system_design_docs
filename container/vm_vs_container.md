# Difference between Virtual Machine and Container

| Virtual Machines | Docker Containers |
| - | - |
| Hardware level process isolation | OS level process isolation |
| VM offers complete isolation of applications from host OS | Docker containers can share some resources with host OS |
| Each VM has separate OS | Each docker container can share OS resources | 
| Boosts in minutes | Boosts in seconds |
More resource usage | Less resource usage
Pre-configured VMs are hard to find and manage | Pre-built docker containers for home server apps already available
Customizing pre-configured VMs required work | Building a custom setup with containers is easy
VMs are typically bigger in size as they contain whole OS udnerneath | Docker containers are small in size with only docker engine over the host OS
VMs can be easily moved to a new host OS | Containers are destroyed and recreated rather than moving
Creating VMs take relatively long time | Docker containers can be created in seconds
Virtualized Apps are harder to find and it takes more time to install and run them | Containerized Apps such as Sonarr, CouchPotatoa etc. can be found and installed easily within minutes

## Reference
1. https://middleware.io/blog/containerization-vs-virtualization/