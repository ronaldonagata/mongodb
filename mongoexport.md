mongoexport --host="IP:PORTA" --authenticationDatabase="admin" --username="" --password='' --collection="Request" --db=logistics --out=events.json --query '{"statistics.availability": "AVAILABLE",date: {$gte: ISODate("2024-03-24T00:00:00.000Z"),$lte: ISODate("2024-03-24T23:59:59.000Z")}}'

mongoexport --uri="mongodb://user:password@cloudapp.azure.com:27017/logistics?readPreference=secondary" --authenticationDatabase="admin" --collection="Request" --type="csv" --out="archiveoptions.json" --fields="info" --query '{"date": { "$gte": { "$date": "2024-03-25T10:00:00.000Z" } } }'

mongoexport --uri="mongodb://10.208.0.106:27017/broker-fulfillment-logistics?readPreference=secondary" --authenticationDatabase="admin" --username="bfladmin" --password='bfladmin2K20!' --collection="deliveryOptionsRequest" --type="csv" --out="Archiveoptions.json" --fields="fieldInfo" --query '{"date": { "$gte": { "$date": "2024-03-25T10:00:00.000Z" } } }'

* https://www.mongodb.com/developer/products/mongodb/mongoimport-guide/
* https://www.mongodb.com/docs/database-tools/installation/installation-macos/
* https://www.mongodb.com/docs/database-tools/mongoexport/
* https://www.mongodbtutorial.org/mongodb-tools/mongoexport/
* https://www.mongodb.com/docs/database-tools/mongoexport/
* https://www.mongodb.com/developer/products/mongodb/mongoimport-guide/
