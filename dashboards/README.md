# Using Grafana as a Sensor Dashboard
1. First set up a connection to [Keepy DB](https://github.com/iot2tangle/Keepy). This option is under Settings > Data Sources

![image](https://user-images.githubusercontent.com/51343893/100308710-43776580-2f66-11eb-9f80-f84a177a8ca0.png)

2. Create a new Dashboard and add a new pannel to it. You can adjust the following queries to quickly add the json data from your sensors.

## Soil Humidity
```
SELECT tt.id as time_sec,tt.metric,
       CAST(tt.value AS DECIMAL(10,2)) as value
FROM (SELECT
  CONVERT((json_extract(message,'$.timestamp')), UNSIGNED INTEGER ) as id,
 (json_extract(message,'$.iot2tangle[2].data[0].SoilHumidity')) as value,
  "Percentage" as metric
FROM messages) tt
WHERE tt.id > 1605812340
ORDER BY tt.id ASC
```
## Air Humidity
```
SELECT tt.id as time_sec,tt.metric,
       CAST(tt.value AS DECIMAL(10,2)) as value
FROM (SELECT
  CONVERT((json_extract(message,'$.timestamp')), UNSIGNED INTEGER ) as id,
 (json_extract(message,'$.iot2tangle[1].data[1].Humidity')) as value,
  "Percentage" as metric
FROM messages) tt
WHERE tt.id > 1605193200
ORDER BY tt.id ASC
```
## Temperatue
```
SELECT tt.id as time_sec,tt.metric,
       CAST(tt.value AS DECIMAL(10,2)) as value
FROM (SELECT
  CONVERT((json_extract(message,'$.timestamp')), UNSIGNED INTEGER ) as id,
 (json_extract(message,'$.iot2tangle[1].data[0].Temperature')) as value,
  "Celcius" as metric
FROM messages) tt
WHERE tt.id > 1605193200
ORDER BY tt.id ASC
```
## Water Pump Status
```
SELECT tt.id as time_sec,tt.metric,
       CAST(tt.value AS DECIMAL(10,2)) as value
FROM (SELECT
  CONVERT((json_extract(message,'$.timestamp')), UNSIGNED INTEGER ) as id,
 (json_extract(message,'$.iot2tangle[3].data[0].WaterPump')) as value,
  "Status" as metric
FROM messages) tt
WHERE tt.id > 1606330740
ORDER BY tt.id ASC
```
## Preassure
```
SELECT tt.id as time_sec,tt.metric,
       CAST(tt.value AS DECIMAL(10,2)) as value
FROM (SELECT
  CONVERT((json_extract(message,'$.timestamp')), UNSIGNED INTEGER ) as id,
 (json_extract(message,'$.iot2tangle[1].data[2].Pressure')) as value,
  "Psi" as metric
FROM messages) tt
WHERE tt.id > 1605193200
ORDER BY tt.id ASC
```