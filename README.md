# docker_wordpress
3 containers - mysql, certbot and wordpress
The purpose for this repo is to document now how to create a wordpress environment with letsecncrypt SSL certs.
There are 2 parts of this operation, before the generation of SSL certs and after the generation of SSL certs.
letsencrypt.org must talk to port 80 prior to the generation of SSL certs. For that reason we would have a nginx.conf file to deal with this aspect of the operation.
After the generation of SSL certs, we would have a nginx.conf file to safeguard our nginx server.
First create a directory mkdir -p /dev/nginx-conf
I had uploaded the files, and rename the docker-compose.yml.orig to docker-compose.yml and similarly rename nginx.conf.orig to nginx
Rename env.txt to .env and replace the parameters to your liking
Once you had done the above in the root directory (/dev) and run docker-compose up -d
Doing docker ps, we should 2 containers are running and certbot container exit with a 0.
Once that is done, amend docker-compose.yml according to docker-compose.yml.ssl - basically replace certbot --staging to --force-renewal and uncomment 443
We would do docker-compose up --force-recreate --no-deps cerbot
This will allow certbot to obtain a real certs instead of the staging certs.
We would now rename nginx.conf.ssl to nginx.conf
We would do docker-compose up --force-recreate --no-depts webserver
With that we should be able to reach wordpress initial configuration screen
I had included a crontab example for the renewal of SSL certs
I had also included a phpmyadmin command - my recommendation is that use it when you need it, as phpmyadmin represents a security risk
