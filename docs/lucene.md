# Lucene Queries

OpenSearch Dashboards supports Lucene queries which is native query as OpenSearch is created on
top of Apache Lucene. You can select the language while querying in **Discover** (_see:_ the button at the end of the
top search bar)

To perform a free text search simply enter a text string. 

```lucene
osx
```

If you search for specific values,

```lucene
response:200
```

If you want to filter the 4xx errors, you can use range queries. Please note, the range keyword. **`TO`** is case-sensitive.

```lucene
response:[400 TO 499]
```

You can match against a set of values

```lucene
response:(404 OR 503)
response:(404, 503)
```

You can use `AND`, `OR` and `NOT` logical operators. If you want to filter out error (non 200 response code)
from `osx`

```lucene
response:(NOT 200) AND machine.os:osx
-response:(200) + machine.os:osx
```

With lucene, you can match a string with fuzziness

```lucene
agent:moizila~
```

You can also check if the data is available with `_exists_` operator

```lucene
_exists_:memory
```

When matching text, you can also use [regular expression](https://www.elastic.co/guide/en/elasticsearch/reference/8.5/regexp-syntax.html)
