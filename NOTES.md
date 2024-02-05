# create a Text index

> db.rent.createIndex({space: 'text'})
> db.rent.find({$text: {$search: 'Tribeca'}})

