Step #1 - Get into a MongoDB pod

```shell
kubectl exec -it mongo-0 mongo
```

Step #2 - Use admin db

```shell
use admin
```

Step #3 - Initiate a Replicaset

```shell
rs.initiate({
"_id" : "zemuldo",
"version":1,
"members" : [
{
"_id" : 0,
"host" : "mongo-0.mongo-headless.z-site.svc.cluster.local:27017",
"priority" : 10
},
{
"_id" : 1,
"host" : "mongo-1.mongo-headless.z-site.svc.cluster.local:27017",
"priority" : 9
},
{
"_id" : 2,
"host" : "mongo-2.mongo-headless.z-site.svc.cluster.local:27017",
"arbiterOnly" : true
}
]
},{force : true});
```

Step #4 - Create admin user

```shell
db.createUser({
user:'admin', pwd:'E0P2O1m-JaAn2AMranJY-9CRSkq9ocfzVHMkdKD', roles : [{role:'root', db:'admin'}]
});
```

Step #5 - Auth with admin user

```shell
db.auth('admin','E0P2O1m-JaAn2AMranJY-9CRSkq9ocfzVHMkdKD');
```

Step #6 - Create admin user in zemuldo db

```shell
use zemuldo-site
```

```shell
db.createUser({
user:'admin', pwd:'E0P2O1m-JaAn2AMranJY-9CRSkq9ocfzVHMkdKD', roles : [{role:'dbAdmin', db:'zemuldo-site'},{role:'readWrite', db:'zemuldo-site'}]
});
```

Step #6 - Delete Stateful set.

```shell
kubectl delete statefulset mongo
```

Step 7
Add auth flag to MongoDB and create stateful set again.