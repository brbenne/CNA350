Pre-Work:
Have a VM with docker, docker-compose, and phpmyadmin installed


Prune docker before starting:
docker system prune -a


Clone repo to VM:
git clone https://github.com/brbenne/CNA350

Change directory:
cd CNA350/maxscale

Ensure docker-compose.yml has lastes version for mariadb, "image: mariadb:10.3" to "image: mariadb:latest":
sudo nano docker-compose.yml

start containers:
sudo docker-compose -f "docker-compose.yml" up -d --build

Confirm Shard-A and Shard-B are Running:
docker-compose exec maxscale maxctrl list servers

Install requirements to use mysql commands:
sudo apt install mariadb-client-core-10.1

Confirm databases:
mysql -u maxuser -pmaxpwd -h 127.0.0.1 -P 3306 -e "show databases"

Query Shards/Zipcodes:
TEST Zipcode1:
mysql -u maxuser -pmaxpwd -h 127.0.0.1 -P 3306 -e "SELECT *  FROM zipcodes_one.zipcodes_one LIMIT 50;"

TEST Zipcode2:
mysql -u maxuser -pmaxpwd -h 127.0.0.1 -P 3306 -e "SELECT *  FROM zipcodes_two.zipcodes_two LIMIT 50;"
