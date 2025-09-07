📘 MongoDB CRUD Operations – README

This guide explains CRUD (Create, Read, Update, Delete) operations in MongoDB with practical examples.

## 1. Database & Collection Setup
   
test> use library
switched to db library
library> db.books.insertMany([{ title: "The Alchemist", author: "Paulo Coelho", year: 1988, genres: ["Fiction", "Philosophy"], available: true, copies: 5 },
...   { title: "Atomic Habits", author: "James Clear", year: 2018, genres: ["Self-help"], available: true, copies: 10 },
...   { title: "Clean Code", author: "Robert C. Martin", year: 2008, genres: ["Programming"], available: false, copies: 0 },
...   { title: "Harry Potter", author: "J.K. Rowling", year: 1997, genres: ["Fantasy", "Adventure"], available: true, copies: 7 }
... ])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('68bce9485571553e13735189'),
    '1': ObjectId('68bce9485571553e1373518a'),
    '2': ObjectId('68bce9485571553e1373518b'),
    '3': ObjectId('68bce9485571553e1373518c')
  }
}

## 2.READ Operations
library> db.books.find()
[
  {
    _id: ObjectId('68bce9485571553e13735189'),
    title: 'The Alchemist',
    author: 'Paulo Coelho',
    year: 1988,
    genres: [ 'Fiction', 'Philosophy' ],
    available: true,
    copies: 5
  },
  {
    _id: ObjectId('68bce9485571553e1373518a'),
    title: 'Atomic Habits',
    author: 'James Clear',
    year: 2018,
    genres: [ 'Self-help' ],
    available: true,
    copies: 10
  },
  {
    _id: ObjectId('68bce9485571553e1373518b'),
    title: 'Clean Code',
    author: 'Robert C. Martin',
    year: 2008,
    genres: [ 'Programming' ],
    available: false,
    copies: 0
  },
  {
    _id: ObjectId('68bce9485571553e1373518c'),
    title: 'Harry Potter',
    author: 'J.K. Rowling',
    year: 1997,
    genres: [ 'Fantasy', 'Adventure' ],
    available: true,
    copies: 7
  }
]

## 3.READ Operations
library> db.books.findOne({author:'J.K. Rowling'})
{
  _id: ObjectId('68bce9485571553e1373518c'),
  title: 'Harry Potter',
  author: 'J.K. Rowling',
  year: 1997,
  genres: [ 'Fantasy', 'Adventure' ],
  available: true,
  copies: 7
}

## 4.UPDATE Operations
library> db.user.update({year:1997},{$set:{year:2000}})
DeprecationWarning: Collection.update() is deprecated. Use updateOne, updateMany, or bulkWrite.
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
library> db.books.update({year:1997},{$set:{year:2000}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

## 5.READ Operations

library> db.books.find()
[
  {
    _id: ObjectId('68bce9485571553e13735189'),
    title: 'The Alchemist',
    author: 'Paulo Coelho',
    year: 1988,
    genres: [ 'Fiction', 'Philosophy' ],
    available: true,
    copies: 5
  },
  {
    _id: ObjectId('68bce9485571553e1373518a'),
    title: 'Atomic Habits',
    author: 'James Clear',
    year: 2018,
    genres: [ 'Self-help' ],
    available: true,
    copies: 10
  },
  {
    _id: ObjectId('68bce9485571553e1373518b'),
    title: 'Clean Code',
    author: 'Robert C. Martin',
    year: 2008,
    genres: [ 'Programming' ],
    available: false,
    copies: 0
  },
  {
    _id: ObjectId('68bce9485571553e1373518c'),
    title: 'Harry Potter',
    author: 'J.K. Rowling',
    year: 2000,
    genres: [ 'Fantasy', 'Adventure' ],
    available: true,
    copies: 7
  }
]

## 6.DELETE Operations

library> db.books.deleteOne({title:'Harry Potter'})
{ acknowledged: true, deletedCount: 1 }
library> db.books.find()
[
  {
    _id: ObjectId('68bce9485571553e13735189'),
    title: 'The Alchemist',
    author: 'Paulo Coelho',
    year: 1988,
    genres: [ 'Fiction', 'Philosophy' ],
    available: true,
    copies: 5
  },
  {
    _id: ObjectId('68bce9485571553e1373518a'),
    title: 'Atomic Habits',
    author: 'James Clear',
    year: 2018,
    genres: [ 'Self-help' ],
    available: true,
    copies: 10
  },
  {
    _id: ObjectId('68bce9485571553e1373518b'),
    title: 'Clean Code',
    author: 'Robert C. Martin',
    year: 2008,
    genres: [ 'Programming' ],
    available: false,
    copies: 0
  }
]

## 7. COUNT Operations
library> db.books.countDocuments()
3

## 8. DISTINCT Operation
library> db.books.distinct('title')
[ 'Atomic Habits', 'Clean Code', 'The Alchemist' ]

## 9.READ operation
library> db.books.find().sort({year:1})
[
  {
    _id: ObjectId('68bce9485571553e13735189'),
    title: 'The Alchemist',
    author: 'Paulo Coelho',
    year: 1988,
    genres: [ 'Fiction', 'Philosophy' ],
    available: true,
    copies: 5
  },
  {
    _id: ObjectId('68bce9485571553e1373518b'),
    title: 'Clean Code',
    author: 'Robert C. Martin',
    year: 2008,
    genres: [ 'Programming' ],
    available: false,
    copies: 0
  },
  {
    _id: ObjectId('68bce9485571553e1373518a'),
    title: 'Atomic Habits',
    author: 'James Clear',
    year: 2018,
    genres: [ 'Self-help' ],
    available: true,
    copies: 10
  }
]
 ## 10.INDEXES
library> db.books.getIndexes()
[ { v: 2, key: { _id: 1 }, name: '_id_' } ]
library> db.books.find({year:{$gte:2001,$lt:2009}})
[
  {
    _id: ObjectId('68bce9485571553e1373518b'),
    title: 'Clean Code',
    author: 'Robert C. Martin',
    year: 2008,
    genres: [ 'Programming' ],
    available: false,
    copies: 0
  }
]
## 11.Comparison && Logical

library> db.books.find({$or:[{year:2018},{year:2020}]})
[
  {
    _id: ObjectId('68bce9485571553e1373518a'),
    title: 'Atomic Habits',
    author: 'James Clear',
    year: 2018,
    genres: [ 'Self-help' ],
    available: true,
    copies: 10
  }
]
library>  db.books.find({$nor:[{year:2018},{year:2020}]})
[
  {
    _id: ObjectId('68bce9485571553e13735189'),
    title: 'The Alchemist',
    author: 'Paulo Coelho',
    year: 1988,
    genres: [ 'Fiction', 'Philosophy' ],
    available: true,
    copies: 5
  },
  {
    _id: ObjectId('68bce9485571553e1373518b'),
    title: 'Clean Code',
    author: 'Robert C. Martin',
    year: 2008,
    genres: [ 'Programming' ],
    available: false,
    copies: 0
  }
]
library> db.books.find({copies:{$exists:true}})
[
  {
    _id: ObjectId('68bce9485571553e13735189'),
    title: 'The Alchemist',
    author: 'Paulo Coelho',
    year: 1988,
    genres: [ 'Fiction', 'Philosophy' ],
    available: true,
    copies: 5
  },
  {
    _id: ObjectId('68bce9485571553e1373518a'),
    title: 'Atomic Habits',
    author: 'James Clear',
    year: 2018,
    genres: [ 'Self-help' ],
    available: true,
    copies: 10
  },
  {
    _id: ObjectId('68bce9485571553e1373518b'),
    title: 'Clean Code',
    author: 'Robert C. Martin',
    year: 2008,
    genres: [ 'Programming' ],
    available: false,
    copies: 0
  }
]
library> db.books.find({copies:{$exists:false}})

## 11. DROP Operations

library> db.books.drop()
true
library> show dbs
admin       40.00 KiB
car         80.00 KiB
config     108.00 KiB
local       40.00 KiB
productdb  108.00 KiB
todo        72.00 KiB
library> use library
already on db library
library> db.books.find()

library> db.dropDatabase()
{ ok: 1, dropped: 'library' }
library> show dbs
admin       40.00 KiB
car         80.00 KiB
config     108.00 KiB
local       40.00 KiB
productdb  108.00 KiB
todo        72.00 KiB
