# Concrete5-docker
A docker image for running your existing concrete5 projects paired with Mariadb in a container. This eliminates the over-head of installing all the various softwares required for the project on your local machine and thus contaminating the system. 

#### Prerequisites
- Docker CE - https://docs.docker.com/get-docker/
- Docker Compose Cli - https://docs.docker.com/compose/install/

#### Installation steps
- Download a zip of the repository
- Extract the zip file
- Now, go ahead and delete the unwanted `.gitignore`, `LICENSE`, `README.md` files so that only the following files are left in the directory
  > images\
  > www\
  > docker-compose.yml
- Alrighty, now its time to clone your project in the `www` directory. 

#### Cloning your project
- The container comes with a default `index.php` file in the `www` directory for testing purposes. You need to setup your actual project in place of this `index.php` file
- `cd` or navigate to `www/` folder 
- Clone your project with the usual `git clone https://xxxxxxx@bitbucket.org/repo.git` command
  > The command will basically create a folder of the repo in the `www` folder. So naturally the url to access your project will be `localhost:[POST]/repo`.
  > If you wish to directly access the content of your project at `localhost:[PORT]` then you can use the `git clone https://xxxxxxx@bitbucket.org/repo.git .` 
  > command. The trailing dot `(.)` in the clone command will clone the contents directly into the `www` directory instead of creating a repo folder in it. 
- Now, `copy+paste` the `config` folder as you would do normally
- Change permission to `777` for the `/www/application/config` directory
  > chmod -R 777 config
- Well the project is setup, now it's time to setup the db. 

#### Connecting application to database:
- Firstly, make sure you change the mysql username and password in the `docker-compose.yml` file
- Point the database host to the `container-name` of the db in your project's `www/application/config/database.php` file
  > In this example it will be `db`. If you do change the container name, then make sure to change the same in your project's `www/application/config/database.php` file
- Done! The app should now be configured to point to the db container mentioned in the `docker-compose.yml` file. 

#### Running your project
- Run the following command to start the project\
`docker-compose up -d`\
This command will start the docker in detached mode (i.e you will not be able to see the debug messages)

- Alternatively, you could also start the docker in attached terminal mode to see the errors in real time with the following command:\
`docker-compose up`. \
To close the attached terminal mode just press `Ctrl + C`

#### Viewing the site in browser
- Once the docker containers are up and running, you could just visit the site by hitting the following urls in your browser based on your preference.
  > `localhost:8070` => PHP 7\
  > `localhost:8056` => PHP 5.6

#### Importing an existing db dump
- Visit `localhost:8000` in your browser
- This will open up the login screen of phpmyadmin. Enter the following credentails:
  > `username: root`\
  > `password: root`
- Once you're logged into phpmyadmin you could easily import and alter your database. 

#### Stoppping the containers
- You can always stop the containers once you're done with the project with the following command:\
`docker-compose down`
