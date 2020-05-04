#Example openHAB solar set up.


```bash
git clone https://github.com/dougculnane/openHAB_solar.git
cd openHAB_solar

# Make a bridge network for our hosts
docker network create solar-openhab

# Run mysql docker container.
docker run --name mysql --net solar-openhab -e MYSQL_ROOT_PASSWORD=openhab -e MYSQL_USER=openhab -e MYSQL_PASSWORD=openhab -e MYSQL_DATABASE=openhab -d mysql:8.0.19

# Build and run openhab docker container.
cd openhab
docker build -t solar-openhab .
docker run --name openhab --add-host=inverter:10.0.1.20 --net solar-openhab -p 8080:8080 -v /etc/localtime:/etc/localtime:ro -d solar-openhab 
cd ..

#  Build and run grafana docker container.
cd grafana
docker build -t solar-grafana .
docker run --name grafana --net solar-openhab -p 3000:3000 -d solar-grafana
cd ..
```

If everything works: http://localhost:8080/habpanel/index.html#/view/Overview

You can browse your data on http://localhost:3000 logging in as user admin and password admin.

You can browse openHAB on http://localhost:8080


