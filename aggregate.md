** Simple GroupBy with count
db.Request.aggregate([
    {"$group" : {_id:{source:"$source",status:"$status"}, count:{$sum:1}}},
    {$sort:{"_id.source":1}}
])

*** Habilitar flag allowDiskUse
db.collection.aggregate([...] ,{allowDiskUse: true});
