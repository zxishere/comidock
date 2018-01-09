# Introduction

LAPP ( Linux, Apache, PostgreSQL, PHP5.6 ) using docker.


### Installation

At first, you should have had [Docker](https://docs.docker.com) and [Docker Compose](https://docs.docker.com/compose) installed.

1 - Clone Comidock:

    git clone https://github.com/zxishere/comidock.git
    
Your folder structure should look like this:

```sh
+ comidock
+ project-1
+ project-2   
```

2 - Go to **apache2/sites**, copy and edit config files to point to different project directory when visiting different domains.

```sh
cp sample.conf.example project-1.conf
```
Edit *.conf DocumentRoot and Directory like


```sh
<VirtualHost *:80>
  ServerName project-1.test
  DocumentRoot /var/www/project-1/public/
  Options Indexes FollowSymLinks

  <Directory "/var/www/project-1/public/">
    AllowOverride All
    <IfVersion < 2.4>
      Allow from all
    </IfVersion>
    <IfVersion >= 2.4>
      Require all granted
    </IfVersion>
  </Directory>

</VirtualHost>
```


3 - Add the domains to the hosts files.

```sh
127.0.0.1  project-1.test
127.0.0.1  project-2.test
...
```

4 - Run your containers:

```sh
cd comidock
docker-compose up -d
```

### Usage

1 - List current running Containers

```sh
docker ps
```

2 - Enter a Container 

```sh
docker exec -it {container-name} bash
```
### Frontend
```sh
docker exec -it comidock_workspace_1 bash
node -v
npm -v
gulp -v
vue -V
yarn -v
```


### Help 

1 - Apache HTTP ERROR 500 : 

```sh
docker exec -it comidock_workspace_1 bash
ls
cd your-project
chmod -R 777 storage bootstrap/cache
```

2 - Laravel .env Connect to PostgreSQL

```sh
DB_CONNECTION=pgsql
DB_HOST=postgres
```
3 - Connect to Mac's Postgres.app

Change the listen_address parameter in the file postgresql.conf:

```sh
listen_addresses '*'
```

Edit the pg_hba.conf file to configure which hosts can access the database

```sh
host all  all    0.0.0.0/0  md5
```
Enter workspace , run:

```sh
docker exec -it comidock_workspace_1 bash
ls
psql -U comiruuser -d comiru_dev -h docker.for.mac.localhost -p 5432
```

**docker.for.mac.localhost** is your mac's ip address in docker container