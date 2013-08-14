## Riak

Riak is an Amazon Dynamo-inspired key/value store that combines a map/reduce
engine, and HTTP/JSON query interface.

  - <http://basho.com/riak/>
  - <http://docs.basho.com/riak/latest/theory/concepts/>
  - <http://docs.basho.com/riak/latest/dev/using/basics/>

## Basho

Basho has an office here in Cambridge and they will also give your team a tech
talk: <http://info.basho.com/SignUpRiakTechTalk.html>

### Create a key/value pair

```bash
curl -i -H "Content-Type: application/json" http://127.0.0.1:8098/riak/mybucket/mykey -d "{\"foo\":\"bar\"}"
```

### Get value of key

```bash
curl -i http://127.0.0.1:8098/riak/mybucket/mykey
```

### Autogenerate a unique key

```bash
curl -i -H "Content-Type: application/json" http://127.0.0.1:8098/riak/mybucket -d "{\"baz\":\"quux\"}"
```

### List all buckets
<http://127.0.0.1:8098/buckets?buckets=true>

### List all keys within a "mybucket" bucket
<http://127.0.0.1:8098/buckets/mybucket/keys?keys=true>

### Manage cluster:
<http://127.0.0.1:8098/admin>

### Link traversal

```bash
curl -i -X PUT -H "Content-Type: text/plain" -H 'Link: </riak/people/tally>; riaktag="friend"' http://127.0.0.1:8098/riak/people/salty -d "Paul"

curl -i -X PUT -H "Content-Type: text/plain" -H 'Link: </riak/people/beardy>; riaktag="friend"' http://127.0.0.1:8098/riak/people/tally -d "Matt"

curl -i -X PUT -H "Content-Type: text/plain" -H 'Link: </riak/people/salty>; riaktag="friend"' http://127.0.0.1:8098/riak/people/beardy -d "Dave"

curl -i -X PUT -H "Content-Type: text/plain" -H 'Link: </riak/people/salty>; riaktag="friend", </riak/people/tally>; riaktag="friend", </riak/people/beardy>; riaktag="friend"' http://127.0.0.1:8098/riak/people/shiny -d "Dave V., iOS magnate"

curl -i http://127.0.0.1:8098/riak/people/beardy/_,friend,_/_,friend,1/
curl -i http://127.0.0.1:8098/riak/people/beardy/_,friend,1/_,friend,1/
```

### Other cool shit (I didn't cover)

  - JavaScript map/reduce queries
  - full-text search
  - secondary index & queries

## Further reading

![](http://imagery.pragprog.com/products/251/rwdata_xlargecover.jpg?1322511067)
[Seven Databases in Seven Weeks, pragprog](http://pragprog.com/book/rwdata/seven-databases-in-seven-weeks)

![](http://ecx.images-amazon.com/images/I/416lDSRBxhL._BO2,204,203,200_PIsitb-sticker-arrow-click,TopRight,35,-76_AA278_PIkin4,BottomRight,-58,22_AA300_SH20_OU01_.jpg)
[Riak Handbook by our friend Mathias @ Travis](http://www.amazon.com/Riak-Handbook-ebook/dp/B009ZIUCJ2)

