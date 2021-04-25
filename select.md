<code> { <field>: { <operator>: <value> }} </code>

$eq is de default operator when an operator is not specified

* Find all documents where the tripduration was less than or equal to 70 seconds and the usertype was not Subscriber:
$ db.trips.find({ "tripduration": { "$lte" : 70 }, "usertype": { "$ne": "Subscriber" } }).pretty()
                
* Find all documents where the tripduration was less than or equal to 70 seconds and the usertype was Customer using a redundant equality operator:
$ db.trips.find({ "tripduration": { "$lte" : 70 }, "usertype": { "$eq": "Customer" }}).pretty()

* Find all documents where the tripduration was less than or equal to 70 seconds and the usertype was Customer using the implicit equality operator:
$ db.trips.find({ "tripduration": { "$lte" : 70 }, "usertype": "Customer" }).pretty()


### Logic Operators

* **$and, $or, $nor, $not**

Find all documents where airplanes CR2 or A81 left or landed in the KZN airport:

db.routes.find({ "$and": [ { "$or" :[ { "dst_airport": "KZN" }, { "src_airport": "KZN" }] }, {"$or" :[ { "airplane": "CR2" }, {"airplane": "A81"}]} ] }).pretty()

db.zips.find( {"$and":[{"pop":{"$lt":1000000}}, {"pop":{"$gt":5000}}]}).count()

### Expressive Query Operator

Find all documents where the trip started and ended at the same station:

db.trips.find({ "$expr": { "$eq": [ "$end station id", "$start station id"] }}).count()

Find all documents where the trip lasted longer than 1200 seconds, and started and ended at the same station:

db.trips.find({ "$expr": { "$and": [ { "$gt": [ "$tripduration", 1200 ]},
                         { "$eq": [ "$end station id", "$start station id" ]}
                       ]}}).count()
                       
                       
Find all documents with exactly 20 amenities which include all the amenities listed in the query array:

db.listingsAndReviews.find({ "amenities": {
                                  "$size": 20,
                                  "$all": [ "Internet", "Wifi",  "Kitchen",
                                           "Heating", "Family/kid friendly",
                                           "Washer", "Dryer", "Essentials",
                                           "Shampoo", "Hangers",
                                           "Hair dryer", "Iron",
                                           "Laptop friendly workspace" ]
                                         }
                            }).pretty()                       

### Query for null values
https://docs.mongodb.com/manual/tutorial/query-for-null-fields/
The { item : null } query matches documents that either contain the item field whose value is null or that do not contain the item field.
<code>db.inventory.find( { item: null } )</code>

The { item : { $exists: false } } query matches documents that do not contain the item field
<code>db.inventory.find( { item : { $exists: false } } )</code>

