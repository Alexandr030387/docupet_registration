# Docupet Registration Challenge

## Getting started
### Before run the container check if you do not use the same ports in the other projects and check if you stop Apache or NGINX
### You can run the next commands without sudo, but if you have the problems with permissions run these commands with `sudo`
* Clone the repository
* Set up docker `sudo apt install docker`
* Set up docker-compose `sudo apt install docker-compose`
* Run the container `sudo docker-compose up -d --build`
* After you built your project, check your container and copy php container and insert to the next command `sudo docker container exec -it php-docupet_registration bash` it can be the same as `php-docupet_registration`
* Run the command above, and you will be inside the container.
* **After that you need to install next packages**:
  * `apt install npm` it is necessary to install yarn 
  * `npm install -g yarn` - yarn installation command
  * also you need to install node, check the version that you use and if it is an old version try to update it `yarn global add n && n 14.15.0`
* If you set up all correct after that run `yarn build` or `yarn watch`