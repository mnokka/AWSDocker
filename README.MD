POC for PostgreSQL database running in docker with automatic db creation in localhost
with adminer db manager to be moved to Amazon Fargate (serverles docker system). 

Only Docker images are needed for AWS ECS usage,they are being pushed to ESC from local machine)

See attached document for AWS ESC deployment steps (DockerToECS_public2.odt)
Rest of this README are talking setting up normal docker-compose based services.

<br>
<br>
Uses Docker host volume mapping in : /home/mika/DOCKERDATA

Uses Docker backups mapping: /DOCKERBACKUPS
<br>
<br>

Start Postgres in docker:

docker-compose up

--------------------------------------------------

Dabatabase creation is executed when docker compose is ran.

Postgress itself does not execute init script if db exists

If existing db is found, initialization is not done

Create db content from host via shell (with override checking):

sudo docker exec -i testipossu psql -U mika -d cars < ./create_db.sql

---------------------------------------------------

Adminer, UI for db management: http://localhost:8100

----------------------------------------------------

Take timestampped db backup:
./backup.sh

----------------------------------------------------

Return backup:
./returnbackup.sh

----------------------------------------------------

Open SQL shell into Docker:
sudo docker exec -it -u postgres testipossu psql -U mika -d cars


------------------------------------------
QT directory includes small Qt(5.15) app to "access" database (showing SELECT * FROM cars;)

Qt Postgres may require driver installation:

sudo apt-get install libqt5sql5-psql libpq-dev
