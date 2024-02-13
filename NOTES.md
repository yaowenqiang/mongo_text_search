# create a Text index

> db.rent.createIndex({space: 'text'})
> db.rent.find({$text: {$search: 'Tribeca'}})

What does $search do

+ Tokenizes
+ Removes stop words
+ Stems
+ Sets to lowercase



if the $search string includes a phrase and individual terms, text search will only match the documents that include the phrase.
> db.rent.find({$text: {$search: "\"bedroom apartment\" sunny"}})


> db.rent.createIndex({'name': 'text'})
> db.rent.find({$text: {$search: 'Tribeca'}}, {'name': 1})
> db.rent.find({$text: {$search: 'Tribeca \"East Village\" -loft'}}, {'name': 1})

# TF-IDF calculation>

> db.rent.find({$text:{$search: 'tribeca loft'}}, {_id: 0, name: 1, score: {$meta: 'textScore'}}).limit(5)

## caseSensitive

> db.rent.find({$text:{$search: 'tribeca Loft', $caseSensitive: true}}, {_id: 0, name: 1 }).limit(5)
> db.rent.find({$text:{$search: 'tribeca Loft', $diacriticSensitive: true}}, {_id: 0, name: 1 }).limit(5)
>
# create compound text index

> db.rent.createIndex({'name': 'text', 'space': 'text'})
>

## create text index on all text fields

db.rent.createIndex({"$**":'text'})


# one text index per collection

## weightedIndex

> db.rent.createIndex({'name': 'text', 'neighbourhood_cleansed': 'text', 'description': 'text'}, {weights: {name: 5, neighborhood_cleansed: 10, description:1}, name: 'my_awsome_index'})
>
> db.rent.find({$text: {$search: 'tribeca loft'}}, {_id:0, name: 1, neighbourhood_cleansed: 1, score: {$meta: 'textScore'}}).sort({score: {$meta: 'textScore'}}).limit(5).pretty()
>
