# Docupet Registration Challenge

## Getting started
### Before run the container check if you do not use the same ports in the other projects and check if you stop Apache or NGINX
### You can run the next commands without sudo, but if you have the problems with permissions run these commands with `sudo`
* Clone the repository
## Before you start to launch your project you need to rename next fields in the next files:
* php/Dockerfile:
  * line 50: `docupet_registration` to the name of your DIR
* nginx/default.conf:
  * line 6: `docupet_registration` to the name of your DIR
* docker-compose.yml:
  * line 6: `docupet_registration` to the name of your DIR
  * line 21: `docupet_registration` to the name of your DIR
  * line 27: `docupet_registration` to the name of your DIR
  * line 33: `docupet_registration` to the name of your DIR
  * line 38: `docupet_registration` to the name of your DIR
## Launch the project
* Set up docker `sudo apt install docker`
* Set up docker-compose `sudo apt install docker-compose`
* Run the container `sudo docker-compose up -d --build`
* In the `app` directory you will find the `.env.example` file, you should copy it and rename to `.env` 
* After you built your project, check your container and copy php container and insert to the next command `sudo docker container exec -it php-docupet_registration bash` it can be the same as `php-docupet_registration`
* Run the command above, and you will be inside the container.
* **After that you need to install next packages**:
  * `composer install` to download all necessary packages and dependencies
  * `apt install npm` it is necessary to install yarn 
  * `npm install -g yarn` - yarn installation command
  * `yarn install` to install all frontend dependencies
  * also you need to install node, check the version that you use and if it is an old version try to update it `yarn global add n && n 14.15.0`
* If you set up all correct after that run `yarn run dev` or `yarn watch`