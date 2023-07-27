# MongoDB Cheat Sheet

## Show All Databases

```
show dbs
```

## Show Current Database

```
db
```

## Create Or Switch Database

```
use acme
```

## Drop

```
db.dropDatabase()
```

## Create Collection

```
db.createCollection('users')
```

## Show Collections

```
show collections
```

## Insert Row

```
db.users.insertOne({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

## Insert Multiple Rows

```
db.users.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```

## Get All Rows

```
db.users.find()
```


## Get Conditional Data
```
db.users.find(
    {$and: 
        [
            {id : 
                {$gt: 5}
            }, 
            {id : {$lt: 7}
            }
        ]
    }
    )


    db.users.find(
        {$or: 
            [
                {id : {$gt: 5}
                }, 
                {id : {$lt: 7}
                }
            ]
        }
        )
```

## Get All Rows Formatted

```
db.users.find().pretty()
```

## Find Rows

```
db.users.find({ category: 'News' })
```

## Sort Rows

```
# asc
db.users.find().sort({ title: 1 }).pretty()
# desc
db.users.find().sort({ title: -1 }).pretty()
```

## Count Rows

```
db.users.find().count()
db.users.find({ category: 'news' }).count()
```

## Limit Rows

```
db.users.find().limit(2).pretty()
```

## Chaining

```
db.users.find().limit(2).sort({ title: 1 }).pretty()
```

## Foreach

```
db.users.find().forEach(function(doc) {
  print("name: " + doc.name)
})
```

## Find One Row

```
db.users.findOne({ category: 'News' })
```

## Find Specific Fields

```
db.users.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```

## Update Row

```
db.users.updateOne({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```

## Update Specific Field

```
db.users.updateOne({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```

## Increment Field (\$inc)

```
db.users.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```

## Rename Field

```
db.users.updateOne({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```

## Delete Row

```
db.users.remove({ title: 'Post Four' })
```

## Sub-Documents

```
db.users.updateOne({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```

## Find By Element in Array (\$elemMatch)

```
db.users.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)
```

## Add Index

```
db.users.createIndex({ title: 'text' })
```

## Text Search

```
db.users.find({
  $text: {
    $search: "\"Post O\""
    }
})
```

## Greater & Less Than

```
db.users.find({ views: { $gt: 2 } })
db.users.find({ views: { $gte: 7 } })
db.users.find({ views: { $lt: 7 } })
db.users.find({ views: { $lte: 7 } })
```
