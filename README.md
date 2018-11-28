Create virtual machine which will have the following
====================================================
- Vagrant file to describe whole components of the machine
- docker for each component
- dockers will be into two categories
    - Non functional dockers like gateway and eureka
    - functional dockers which will have the application code
- docker composer to define the network details

Vagrant file
------------
it will be based on ubuntu machine with docker container installed on it
by using docer provisioner

Non-functional dockers
----------------------
- config service
- eureka service
- gateway service
- authentication service
- ELK stack
- Monitor dashboard
- Jenkins
- Maven Repo
- Docker Repo

Functional dockers
------------------
A list of sample applications which will include
- 3 UI applications
    - Angular
    - reactjs
    - Another Angular
- 5 backend microservices