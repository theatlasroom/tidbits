# Software
Various software I have used, some web based, some not.

## CartoDB
- Allows real time sync of data
- Uses Postgresql + includes some CDB specific functions to make working with data a little bit easier
- Includes [PostGIS](http://postgis.net/) - Open source GIS functions for Postgres DBs

  `/* Creates a new column called distance, converts it from degrees to a geography (converts it to metres) and then divide by 1600 so that it is in miles */
   SELECT *, ST_Distance(the_geom, CDB_LatLng(30.3952962, -97.7374002)::geography)/1600 as distance
   FROM loud_music_austin`

## Tableau
 * Tableau workbooks can be shared
 * Data analysis tool - used to ask questions
   - has best practice visualisations built in
     * Represent data using:
       - position
       - colour
       - shape
       - size
 * Tableau desktop - authoring tool, used to ask question of your data
   - connect live: point tableu to your data source / data warehouse
   - create an extract: offline copy our your data -> copy a subset of your data
   - Integrates directly with R
   - automatically groups data into:
     * dimensions: gender, city, category, country
     * measures: profit, quantity, sales etc
 * Tableau server: controls access to tableau content
