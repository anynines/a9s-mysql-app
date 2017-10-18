# README

```
# start MySQL
docker run --name mariadb -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mariadb:10.1

# install app dependencies and start the server
bundle
bundle exec rake db:setup 
bundle exec rails s
```

Open [http://localhost:3000/](http://localhost:3000/) in your browser.
