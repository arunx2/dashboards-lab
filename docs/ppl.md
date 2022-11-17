## PPL
 PPL is a unix style piped processing language where you can pipe to previous results
In this lesson, we will use the ecommerce data.

- To view all documents from an index 
    ```sql
    search source=opensearch_dashboards_sample_data_ecommerce;
    ```

- To select specific fields
    ```
     search source=opensearch_dashboards_sample_data_ecommerce
   | fields order_id, customer_full_name, taxful_total_price
    ```

- To select documents based on a condition
    ```
    search source=opensearch_dashboards_sample_data_ecommerce
   | where taxful_total_price > 100.00
   | fields order_id, customer_full_name, taxful_total_price
    ```
  
- to dedup based on a field
    ```sql
    search source=opensearch_dashboards_sample_data_ecommerce
    | where taxful_total_price > 100.00
    | dedup customer_gender
    | fields order_id, customer_full_name, taxful_total_price, customer_gender
    ```
- dedup based on customer email.
- create a runtime field.
- sort 
- stats
- aggregation
- joins

Request Format

To use the PPL plugin with your own applications, send requests to _plugins/_ppl, with your query in the request body:

```shell
curl -H 'Content-Type: application/json' -X POST localhost:9200/_plugins/_ppl \
... -d '{"query" : "source=opensearch_dashboards_sample_data_logs | fields url, machine.os"}'
```
```sql
    search source=opensearch_dashboards_sample_data_ecommerce | stats count() as email_count by email | sort -email_count | fields email_count, email
```

```sql
source = opensearch_dashboards_sample_data_ecommerce | stats sum( taxful_total_price ), count() as count by customer_id | sort -count
```