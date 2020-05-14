# weather-dashboard

## Goal

Use **node-red** to store the weather data of 4 cities in an InfluxDB database and show it in a dashboard.

## Running the project

The project uses one environment variable: `OWM_ID`. It is the private user key that you get when subscribing to openweathermap. 

Its value must be set when running node-red:
```bash
OWM_ID=<value2> node-red
```

## Database structure

Node-red package for InfluxDB: `node-red-contrib-influxdb`

We create an InfluxDB database called `weather_db`. The database should contain one measurement called `weather`.

The measurement contains fields and tags.

### Fields

- `temp`: Temperature in [°C]
- `tempFeel`: Temperature in [°C] as perceived by humans
- `humidity`: Humidity in [%]
- `wind`: Wind speed in [m/s]
- `rain`: Amount of rain fallen over last hour in [mm]
- `clouds`: Cloudiness in [%] (I forgot about this one...)

### Tags

- `city`: Location of the measurement
- `weather`: Weather description in a few words

### Retention policies

- log data in the database every minute
- for data >24h, keep 1 entry per hour
