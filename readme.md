# Wordpress Jail Cell.

### Description.
This is a jail cell in which you can run and develop safely a wordpress based project.

It is based on `docker` and make sure [Docker](https://www.docker.com/) is installed on your system.

### Make it work.

- Clone the project.
```sh
> git clone https://github.com/andreiconstantinescu/wp-jail-cell
```

- Make it yours.
```sh
> rm -rf .git && git init
```

- If you have any worpress backups (theme and db), add them in the `backups` folder.
Usually they are in `.tar.gz` and `.sql.bz2` formats.

- Create a folder named `.env` in the root of the clone with the following file structure and contents:
```sh
.env
├── backup.env
├── mariadb.env
└── wp.env
```
  - `backup.env` has the following env vars:
```sh
MYSQL_ENV_MYSQL_USER=<user>
MYSQL_ENV_MYSQL_DATABASE=<database_name>
MYSQL_ENV_MYSQL_PASSWORD=<user_password>
```
  - `mariadb.env` has the following env vars:
```sh
MYSQL_ROOT_PASSWORD=<root_password>
MYSQL_USER=<user>
MYSQL_PASSWORD=<user_password>
MYSQL_DATABASE=<database_name>
```
  - `wp.env` has the following env vars:
```sh
WORDPRESS_DB_NAME=<database_name>
WORDPRESS_DB_PASSWORD=<user_password>
WORDPRESS_DB_USER=<user>
```

- `cd` into the root folder of the clone and start the containers
```sh
> docker-compose up
```
(add `-d` if you want it to run in the background)

If everything is configured correctly, opening [localhost:8080](http://localhost:8080) should ask you to install wordpress. Now, in a new terminal window, providing the `backups` folder is populated, run the restore of the backups.

```sh
> docker exec wp_backup restore <date OR name>
```

- Refresh the page and enjoy using Wordpress from a harmless jail cell 😀

### The rest of the info.
- It uses [MariaDB](https://mariadb.com/) instead of [MySQL](https://www.mysql.com/), which is fully compatible with the `mysql` commands.

- To stop the containers you either `cd` in the project folder and then run
```sh
> docker-compose down
```
(adding `--volumes --remove-orphans` will remove also the DB and a new restore will be necessary)
**OR** run
```sh
> docker stop wp_blog wp_backup wp_db
```

- To rerun the project, cd in the root of the clone and start it
```sh
> docker-compose up
```

- To perform a backup run
```sh
> docker exec wp_backup backup
```

- To change the name of the containers, don't be afraid to open `docker-compose.yml` and edit the `container_name` keys as you wish. Keep in mind to use the new names in the commands that are using them.

- The wordpress theme will live in the `wordpress` folder and whatever modifications are made from through your favourite editor will be reflected on the next refresh of [localhost:8080](http://localhost:8080).

### Todos and PRs.
I am very sure that improvements can be made so don't be afraid to PR them 😁.

### License.
MIT.
