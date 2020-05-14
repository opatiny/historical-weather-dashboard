# weather-dashboard

## Goal

Use **node-red** to store the weather data of 4 cities in an InfluxDB database and show it in a dashboard.

## Run with docker

Refer to the dockerized project: [https://github.com/opatiny/docker-weather-dashboard ](https://github.com/opatiny/docker-weather-dashboard).

## Running the project

The project uses one environment variable: `OWM_ID`. It is the private user key that you get when subscribing to openweathermap. 

Its value must be set when running node-red:
```bash
OWM_ID=<value2> node-red
```

## Database structure

We create an InfluxDB database called `weather_db`. The database contains 3 measurements called `weather`, `weather_hourly` and `weather_daily`.

The measurements contain fields and tags.

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

### Continuous queries

3 different measurements:
- `weather`: log data in the measurement every minute
- `weather_hourly`: query `weather` and aggregate by hour
- `weather_daily`: query `weather` and aggregate by day

