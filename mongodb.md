# mongodb

## Querying

```
db.users
  .aggregate(
   [
      // Match only users in a certain set of towns.
      {
          $match: {town: { $in: ['ripon'] } }
      },
      // Group by town, measure count.
      {
        $group : {
           _id : "$town",
           count: { $sum: 1 }
        }
      }
   ]
)
```

## General DBA

```
show dbs;
show users;
show collections;
show roles;
show profile;
```

## User Management

Create user:

```
use test;
db.createUser(
   {
     user: "accountUser",
     pwd: "password",
     roles: [ "readWrite", "dbAdmin" ]
   }
)
```

Add role:

```
db.grantRolesToUser("accountUser", [{ role: "readWrite", db: "test" }]
```

## Restore

Restore a database dump in a given folder to a db:

```
mongorestore --dir ./dump --host testdb.org.local
```

## Desharding

Desharding is fun. A good guide is [MongoDB - Converting a Sharded Cluster to a Replicaset](https://docs.mongodb.com/manual/tutorial/convert-sharded-cluster-to-replica-set/).

In this example, we have:

- `shard1.mongo-cluster.com`
- `shard2.mongo-cluster.com`
- `shard3.mongo-cluster.com`

First, remove each shard, except for the primary:

```
db.adminCommand( { removeShard: "shard2.mongo-cluster.com" } )
```

This command will return the status of the shard removal - run it repeatedly to get output like this:

```
```

This will also show which databases need to have their primary moved to a new shard:

Remove all dbs which are primary on the third shard:

```
db.runCommand( { movePrimary: "jenius_lending", to: "mongodev1.dev.corp.btpn.co.id" })
```

Now repeat for `shard3`. Once this is done, you are down to one shard only.

## Checking Index Usage

```
db.getCollection('whatever').aggregate( [ { $indexStats: { } } ] )
```
