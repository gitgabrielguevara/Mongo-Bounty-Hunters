# Mongo Bounty Hunters
Title: Intergalactic Bounty Hunter Database<br>
Creator: [Karolin Rafalski](https://generalassemb.ly/instructors/karolina-rafalski/11367) <br>
Adapted From: [WDI Remote - Mongo Lab](https://git.generalassemb.ly/Web-Development-Immersive-Remote/WDIR-Stan-Lee/blob/master/unit_2/w06d02/student_labs/morning.md) <br>

## Intergalactic Bounty Hunter Database

You've been going to meetup events and networking. You've been telling everyone you're so excited to get a dev job that you'll take _any job_.

You run into a shadowy stranger, who asks you three times 'Really? Any job?' and you continue to agree enthusiastically. Things go dark, and you wake up in a strange place.

The shadowy stranger greets you and says 'Welcome to your new job! You are now our dev who will be building an intergalactic bounty hunter database for us!'

You look around, notice some high end coffee and tea machines, an air hockey table, nap rooms and floor to ceiling windows with a view of outer space. The shadowy stranger takes you to your desk which has a fancy sit-to stand adjustable hight desk with a swing bar, two big monitors, and Herman Miller chair. You say to yourself 'Not bad! Not bad at all!'

## Getting Started

* **Fork** and **Clone** this repository!
* Do the assignment!
* To turn this assignment in:
    * Record your terminal command history inside the `answers.txt` file!
    * Push to your fork of the repository
    * Make a **Pull Request** against the base repository

## Set up

Start `Mongo`, by typing `mongod`, if you don't already have it running.

Open a new tab and start a Mongo shell if you don't have it running by typing `mongo`

connect to a new sub-database by typing

```
use hunters
```

> Note: If this database does not exist, it will be created. Yay Mongo!

Let's create a collection for all the beings that have bounties.

```js
db.createCollection('bounties')
```

We should get an `ok` message.

## Create/Insert

Let's add our first bounty

```js

db.bounties.insert(
  {
    name: 'Han Solo',
    wantedFor : 'Owing money',
    client : 'Jabba the Hut',
    reward : 1000000,
    ship: 'Millennium Falcon',
    hunters :['Bobba Fett', 'Dengar', 'IG-88', 'Zuckuss', 'Greedo', 'Bossk', '4-LOM'],
    captured: false
  }
  )
```

You should get an ok message that looks similar to this:

![Insert ok](https://i.imgur.com/KdFh4Ss.png)

Using the above template, make another bounty

Now insert a few more bounties

```js

db.bounties.insert([
  {
    name: 'Han Solo',
    wantedFor : 'Owing money',
    client : 'Jabba the Hut',
    reward : 1000000,
    ship: 'Millennium Falcon',
    hunters :['Bobba Fett', 'Dengar', 'IG-88', 'Zuckuss', 'Greedo', 'Bossk', '4-LOM'],
    captured: false
  },
  {
    name: 'Rocket',
    wantedFor : 'Stealing Batteries',
    client : 'Ayesha High Priestess of the Sovereign',
    reward : 1000000000,
    ship: 'The Milano',
    hunters :['Nebula', 'Ravagers'],
    captured: false
  },
  {
    name: 'Sara Lance',
    wantedFor : 'Screwing up the timeline, causing anachronisms',
    client : 'Time Bureau',
    reward : 50000,
    ship: 'Waverider',
    hunters :['Chronos'],
    captured: false
  },
  {
    name: 'Malcolm Reynolds',
    wantedFor : 'Aiming to misbehave',
    client : 'The Alliance',
    reward : 40000,
    ship: 'Serenity',
    hunters :['Jubal Early'],
    captured: false
  },
  {
    name: 'Starbuck',
    wantedFor : "Disobeying Captain's orders",
    client : 'Captain Adama',
    ship: 'Demetrius',
    reward : 1000,
    hunters :['Apollo'],
    captured: true
  }
])
```

## Read/Query

- Do a query to see all the bounties
db.bounties.find({})
- Do a query to find the bounty whose client is `Time Bureau`

db.bounties.find({ client: 'Time Bureau' })
- Do a query to find the bounties who have been `captured`

db.bouties.find({captured:true})

- Do a query specific to the bounty you inserted

db.bouties.find({name: 'Gabe'})
- Do a query to just return the names of all the bounties

db.bounties.find({},{name:true}).pretty()
## Remove

- Starbuck and the Captain have come to an understanding. Remove her record

db.bounties.find({},{name:true}).pretty()
- find and remove the duplicate record - be sure to JUST remove the one copy

## Update

Update `Sara Lance`'s name to be her superhero alias 'White Canary'

db.bounties.update({name:'Sara Lance'},{$set:{name:'White Canary'}})

Update Rocket's ship to be `The Milano 2`

db.bounties.update({name:'Rocket'},{$set:{name:'The Milano 2'}})
### Intermediate Mongo

Check out the [Intermediate Mongo](https://gawdiseattle.gitbook.io/wdi/04-databases/mongo-intro/intermediate) lecture notes in the instructor notes directory. Follow through each of the explanations. Follow the commands and perform appropriate finds after each update call to see the results

- Find the bounties that are greater than `100000`
db.bounties.find({reward:{$gt:100000}}).pretty()

- Find the bounties that are less than `1000`
db.bounties.find({reward:{$lt:1000}}).pretty()

- Find the bounties that are less than or equal to `1000`
db.bounties.find({reward:{$lte:1000}}).pretty()

- Find the bounty with the hunter `Nebula`
db.bounties.find({hunters: 'Nebula'})

- Find the bounty with the ship `Waverider` OR `Serenity`

- Find the bounty who is not captured AND has whose client is `Ayesha High Priestess of the Sovereign`
db.bounties.find({captured: false},{client:`Ayesha High Priestess of the Sovereign` })

- Increase all the bounties by 333333
db.bounties.update({ $inc: {reward: 33333}},{multi: true})

- Multiply all the bounties by 2
- Add `Bobba Fett` as a hunter for `Malcolm Reynolds`

db.bounties.update({ $inc: {reward: 33333}},{multi: true})
- Add `Bobba Fett` as a hunter for the one that has the ship `Waverider`
db.bounties.update({ $inc: {reward: 33333}},{multi: true})

- Find and remove `Dengar` the bounty hunter


- Upsert is used with update method which creates a new document if the query does not retrieve any documents matching the query parameters.
- Try giving a `lastSeen` field to Han Solo, with the property `yesterday` (we haven't set his yet)
- Try giving all bounties that are not Han Solo a new field of `lastSeen` - with a value of `last week`

## Turn It In!

Put your terminal output (let's say the last 50 lines or so, not everything you ever did!) into the file in this directory called `answers.txt`. Commit and push your changes, then make a pull request against the base fork.

Get your Mongo shell history with the following command: `tail -50 ~/.dbshell`

Did you have any questions or comments about this deliverable? Please add it to the text of your pull request!

### That's it! You're all done!

Ahh... time to relax!

![Relax](https://media.giphy.com/media/hR7yR2AMVxv8c/giphy.gif)

