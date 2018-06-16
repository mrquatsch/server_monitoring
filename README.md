# Server monitoring configuration

#### Configuration items:
* telegraf
* influxdb
* grafana
* custom python script for plexpy export

### How...
* **InfluxDB**
	* [https://hub.docker.com/_/influxdb/](https://hub.docker.com/_/influxdb/)
		* `docker run -d -p 8086:8086 -v <local influx db directory>:/var/lib/influxdb --name=influxdb --restart=always influxdb`

* **Telegraf**
	* Download app
		* [https://portal.influxdata.com/downloads](https://portal.influxdata.com/downloads)
	* Use conf supplied here
		* `/etc/telegraf/telegraf.conf`
	* I used Ubuntu...
		* `sudo apt-get install telegraf`
		* `sudo  systemctl enable telegraf`
		* `sudo systemctl start telegraf`
* **Grafana**
	* [https://hub.docker.com/r/grafana/grafana/](https://hub.docker.com/r/grafana/grafana/)
		* `docker run -d -e "GF_SECURITY_ADMIN_PASSWORD=secret" -p 3000:3000 --name=grafana -v grafana-storage:/var/lib/grafana --restart=always grafana/grafana`
		* Other docker configurations covered here - [http://docs.grafana.org/installation/docker/](http://docs.grafana.org/installation/docker/)
	* Create two datasources
		* plexpy & telegraf are the influxdb database names
	* Import dashboard json
* **InfluxDB Plexpy export**
	* Use plexpy_influxdb_export.py
		* Taken from [https://github.com/Drewster727/tautulli-influxdb-export](https://github.com/Drewster727/tautulli-influxdb-export)
		* View Drewster727's repo for run examples
		* FYI: My script is slightly modified to pull in a few more bits of data
	* If using ubuntu, my plexpy_influxdb_export.service service file can be used. You'll just need to review Drewster727's repo for the appropriate options to use.
