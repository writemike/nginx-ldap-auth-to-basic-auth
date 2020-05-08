# nginx-ldap-auth-to-basic-auth

I started with [nginx-ldap-auth demo](https://github.com/nginxinc/nginx-ldap-auth) which uses NGINX with a Python Backend Web Server, OpenLDAP, and a Translational LDAP Python Daemon.
 
I modified it by running everything in 4 Docker Containers and used my Laptop as the Client.
1. Client – MacBook
     * For testing and reviewing logs from containers
2. NGINX OSS – Latest Docker Container (from Dockerhub)
     * Responsible for traffic routing based on Authentication status
3. ldap-auth-daemon – Running in latest Python3 Docker Container (from Dockerhub)
     * Converts HTTP request into and LDAP Auth Request for LDAP Server Validation
4. LDAP Server - Running in latest OpenLDAP Docker Container with prepopulated user data (from Dockerhub)
     * Stores and validates user credentials
5. Backend Daemon - Running in latest Python3 Docker Container (from Dockerhub)
     * Represents Web Server which provides login page as well as actual website once authentication is completed successfully.

## Getting Started

```shell
$ docker-compose up -d
Creating network "nginx-ldap-auth-to-basic-auth_default" with the default driver
Creating nginx-ldap-auth-to-basic-auth_nginx_1             ... done
Creating nginx-ldap-auth-to-basic-auth_nginxweb_1          ... done
Creating ldap_auth_daemon                                  ... done
Creating ldap_server                                       ... done
Creating backend_app                                       ... done
Creating nginx-ldap-auth-to-basic-auth_ldap_server_admin_1 ... done
$ docker ps
CONTAINER ID        IMAGE                                     COMMAND                  CREATED             STATUS              PORTS                              NAMES
091c42349e51        writemike/backend-sample-app:python       "python3 -u /usr/src…"   16 seconds ago      Up 15 seconds       127.0.0.1:9000->9000/tcp           backend_app
9cd825aa4cdc        osixia/phpldapadmin:0.7.2                 "/container/tool/run"    16 seconds ago      Up 15 seconds       443/tcp, 0.0.0.0:8090->80/tcp      nginx-ldap-auth-to-basic-auth_ldap_server_admin_1
b62eceea65d5        writemike/nginx-ldap-auth-daemon:python   "python -u /usr/src/…"   16 seconds ago      Up 15 seconds       127.0.0.1:8888->8888/tcp           ldap_auth_daemon
fbe63e5dc44a        writemike/openldap:withdata               "/container/tool/run"    16 seconds ago      Up 15 seconds       0.0.0.0:389->389/tcp, 636/tcp      ldap_server
a5c17f7a8171        nginx:stable                              "nginx -g 'daemon of…"   16 seconds ago      Up 15 seconds       80/tcp, 127.0.0.1:8082->8082/tcp   nginx-ldap-auth-to-basic-auth_nginxweb_1
03591e506a13        nginx:stable                              "nginx -g 'daemon of…"   16 seconds ago      Up 15 seconds       80/tcp, 127.0.0.1:8081->8081/tcp   nginx-ldap-auth-to-basic-auth_nginx_1 ```
