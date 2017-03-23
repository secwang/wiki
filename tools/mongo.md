---
title: "mongo"
date: 2016-11-25 23:00
---
[TOC]

## update key name

db.types.updateMany({}, { $rename : { 'Table 1' : 'type' ,'':'link'} } ) 

## find things
db.types.find

## update emptykey
do not try to create such key.

## drop table or collection
db.types.drop

## mongo imoprt csv
mongoimport -d mydb -c things --type csv --file locations.csv --headerline


## mongo find like
db.users.find({"name": /m/})

## mongo dump

mongodump --db=<old_db_name> --collection=<collection_name> --out=data/

mongorestore --db=<new_db_name> --collection=<collection_name> data/<db_name>/<collection_name>.bson

