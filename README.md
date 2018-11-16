# a9s MySQL sample app

This app implements a very simple blogging app to showcase our a9s MySQL service on CloudFoundry. It is based on [Ruby on Rails](https://rubyonrails.org/) 5.1. The most interesting part is most likely the [manifest](manifest.yml) which is used to give the CF cli information about your app. Please [this page](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html) for more information.

## Pushing the app CloudFoundry

Register on [paas.anynines.com](https://paas.anynines.com) to obtain an account which allows you to push your app. After, you created the account and targeted (cf target ...) the desired org/space, execute the following steps (this create a **small** MySQL service instance):

```shell
cf create-service a9s-mysql101 mysql-single-small mysql1
... <wait for service to be created> ...
cd <path to>/a9s-mysql-app
... edit the manifest.yml and replace the name of the service in the 'services:' field ...
cf push
```

This uses the mysql-single-small plan for a **small, non-replicated** MySQL server. Use the following command to find out which plans are available:

```shell
cf marketplace -s a9s-mysql101
```

### NOTE

If you push/start the app before the service is available, it will fail because it assumes a MySQL database server to be available.

## Using docker

```shell
# start MySQL
docker run --name mariadb -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mariadb:10.1

# install app dependencies and start the server
bundle
bundle exec rake db:setup
bundle exec rails s
```

Open [http://localhost:3000/](http://localhost:3000/) in your browser.
