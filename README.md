# nginx-ldap-auth-to-basic-auth

I started with nginx-ldap-auth demo (https://github.com/nginxinc/nginx-ldap-auth) which uses NGINX with a Python Backend Web Server, OpenLDAP, and a Translational LDAP Python Daemon.
 
I modified it by running everything in 4 Docker Containers and used my Laptop as the Client.
1. Client – MacBook
      For testing and reviewing logs from containers
2. NGINX OSS – Latest Docker Container (from Dockerhub)
      Responsible for traffic routing based on Authentication status
3. ldap-auth-daemon – Running in latest Python3 Docker Container (from Dockerhub)
      Converts HTTP request into and LDAP Auth Request for LDAP Server Validation
4. LDAP Server - Running in latest OpenLDAP Docker Container with prepopulated user data (from Dockerhub)
      Stores and validates user credentials
5. Backend Daemon - Running in latest Python3 Docker Container (from Dockerhub)
      Represents Web Server which provides login page as well as actual website once authentication is completed successfully.
                                  
