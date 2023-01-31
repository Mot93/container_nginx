# Building a nginx custom image
In this repo there is all the necessary files to build a custom nginx image.

The Dockerfile [compiles and install all the dependencies from source](https://docs.nginx.com/nginx/admin-guide/installing-nginx/installing-nginx-open-source/). 
Before building the image, download all necessary packages using the `download_libraries.sh` bash script.

To add nginx module, add them at the configure in the last `RUN` of the `Dockerfile`.

# How to
***Build***:

    docker compose build

***Run the container and expose port 80 on 8080***:

    docker compose run

Got to [localhost:8080](http://localhost:8080) to view the welcome page
