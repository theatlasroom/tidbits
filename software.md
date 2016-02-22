# Software
Various software I have used, some web based, some not.

## CartoDB
- Allows real time sync of data
- Uses Postgresql + includes some CDB specific functions to make working with data a little bit easier
- Includes [PostGIS](http://postgis.net/) - Open source GIS functions for Postgres DBs

  `/* Creates a new column called distance, converts it from degrees to a geography (converts it to metres) and then divide by 1600 so that it is in miles */
   SELECT *, ST_Distance(the_geom, CDB_LatLng(30.3952962, -97.7374002)::geography)/1600 as distance
   FROM loud_music_austin`
