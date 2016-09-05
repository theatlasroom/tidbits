# MongoDB
## Commands
* mongod - start mongodb server daemon
* mongo - connect to the mongodb
* mongodump -d <database> -c <collection - optional> -o <output-file> - export database to file 
* mongoimport - import file to database collection
* mongorestore - restore db from dump

## Dokku
* dokku mongo:export - export db dump to tar
* dokku mongo:import - import db dump from tar (tar without the -z option)

## General
* `use db` - switch to a database
* `show dbs|collections` - show database / collections
* Shutdown mongo: `use admin` then `db.shutdownServer()`

## Queries
* db.collection.find()
* db.collection.findOne()
