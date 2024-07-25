# MongoDB Cheat Sheet

# Using this command for show All Databases 
show dbs

# Show Current Database
db

# Create a new or switch databases
use dbname

# Drop
db.dropDatabase()

# Create Collection
db.createCollection('posts')

# Show Collections
show collections

# Drop a collection named 'posts'
db.posts.drop()

# Insert Row
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  
  tags: ['news','events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})

# Insert many Rows

db.posts.insertMany([
    {
    'name': 'Harry',
    'lang': 'JavaScript',
    'member_since': 5
    }, 
    
    {'name': 'Rohan',
    'lang': 'Python',
    'member_since': 3
    },
    
    {'name': 'Lovish',
    'lang': 'Java',
    'member_since': 4
}])

# Get All Rows
db.posts.find()

# Show all Rows in a Collection (Prettified)
db.posts.find().pretty()

# Find Rows
db.posts.find({ category: 'News' })

# Find the first row matching the object
db.posts.findOne({name: 'Harry'})

# Limit the number of rows in output
db.comments.find().limit(2)


# Sort Rows
# asc
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()

# Count Rows
db.posts.find().count()
db.posts.find({ category: 'news' }).count()

# Limit Rows
db.posts.find().limit(2).pretty()

# Chaining
db.posts.find().limit(2).sort({ title: 1 }).pretty()

# Foreach
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})

# Find One Row
db.posts.findOne({ category: 'News' })

# Find Specific Fields
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})

# Update a row
db.posts.updateOne({name: 'Shubham'},
{$set: {'name': 'Harry',
    'lang': 'JavaScript',
    'member_since': 51
}}, {upsert: true})

# Update Specific Field
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
# Increment Field ($inc)
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})

# Rename Field
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})

# Delete Row
db.posts.remove({ title: 'Post Four' })

# Greater & Less Than
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })

# Sub-Documents
db.posts.update({ title: 'Post One' },
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

# Find By Element in Array ($elemMatch)
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)


# Add Index
db.posts.createIndex({ title: 'text' })
Text Search
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})



