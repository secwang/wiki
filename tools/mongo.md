<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [update key name](#update-key-name)
- [find things](#find-things)
- [update emptykey](#update-emptykey)
- [drop table or collection](#drop-table-or-collection)
- [mongo imoprt csv](#mongo-imoprt-csv)
- [mongo find like](#mongo-find-like)
- [mongo dump](#mongo-dump)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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

