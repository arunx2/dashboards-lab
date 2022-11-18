
## DQL

Similar to the [Query DSL](https://opensearch.org/docs/1.3/opensearch/query-dsl/index) that
lets you use the HTTP request body to search for data, you can use the Dashboards Query
Language (DQL) in OpenSearch Dashboards to search for data and visualizations. Please note that
it only filters data, and you can neither do aggregation, sorting nor any transformations

There are four major types of queries you can run in DQL
### Filter with matches
Basic query type matches a value against a field in the document.

```text
field: value
```
You can match both `field` and `value` with wildcards like this
```text
geo.*: AR
```
You can also use wild card to filter events

```text
url: *www.opensearch.org*
```
### Filter with a range
If you have numeric, IP address, geo_point, or date values, you can use comparators to
compare against another value. The supported comparators are
- `<`  less than
- `>` greater than
- `<=` less than or equal to
- `>=`, greater than or equal to

### Compound queries
You can construct compound queries with `and`, `or`, and `not` operators. These are case-insensitive
so `NOT` and `not` are same.

### Nested fields queries
With DQL, you can query the nested objects with `{}` .

## Examples 
Make sure you select `opensearch_dashboards_sample_data_logs` as **Index Pattern** in the top left,
to execute the below samples.
- You can do a simple search matches any value across fields in the index, To list all events related to `Firefox` 
  ```text
    Firefox
  ```
  To list events related to `Firefox` or `osx`
  ```sql
    Firefox or osx
  ```
  Plain search can quickly help you find things without knowing much about the schema. But if you know 
  the schema you can better control your searches.

- In the sample logs, the user agent is captured in `agent` attribute. If you want to filter out `Linux`. you can use
  ```text
    agent: Linux
  ```
- If you want to select events that transferred over 2000 bytes
  ```text
    bytes > 2000
  ```
- If you want to select events that are generated from `Linux` server and transferred over 2000 bytes
  ```text
    agent: Linux AND bytes > 2000
  ```
- If you want to filter events with `phpmemory` field exists
  ```text
    phpmemory : *
  ```
- you can match with multiple terms with sets. The below query matches the events
  if it comes from either `ios` or `osx`
    ```text
    machine.os: (osx,ios)
    ```
  
## Exercises

1. Find out all events which are not originated from Linux. (_Hint: use NOT operator_ )
2. Find out all events, originated from the Netherlands. (_Hint: geo.src has the two letter origin country value **NL**_)
3. Filter out events that doesn't have `memory` field.
4. Find out all events between India (IN) and Japan(JP)

You can find answers [here](./solutions.md#dql-exercise-solutions)
