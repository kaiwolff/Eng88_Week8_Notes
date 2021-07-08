Docker-compose files allow us to pre-configure a docker container, for example, by setting up a link between several ports

Docker compose works on the idea of services. Microservices can have several containers. define a variable called "services:"

Written in a yml file, which depends on indentation (similarly to python). See the docker-compose file in this directory for an example.

Can run docker-compose up to start the container. The -d option will run the container as a daemon.

Can use the container_name variable to set a particular name for the container when the app has been run. This allows the deployment of a set of functions wiht a desired name.

If something such as a password is needed, this can be set ot be received only when the container is being run.  Defining environment variables makes them accessible via bash, which allows a bash script to alterthem if this step needs automating (of course, never push a script with passwords to git).

Can even set up networks to link different ocntianers. We will likely be using this to link the sql database to the main webapp.

To store data in a way that means it is reatained after the container is shut down, we set up volumes, in the format [storage_filepath]:[container_filepath]