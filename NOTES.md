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

> "sunny bedroom apartment" == "apartment" OR "bedroom" OR "sunny"

"sunny \"bedroom apartment\"  " == "(sunny OR bedroom OR apartment)" AND "bedroom apartment"

"bedroom apartment"  == "bedroom" OR "apartment"

"bedroom -apartment" == "bedroom" AND NOT "apartment"

"bedroom-wrecker -apartment" == "apartment-wrecker" AND NOT "apartment"

