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
