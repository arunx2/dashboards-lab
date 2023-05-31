# Solutions

## DQL Exercise Solutions

1. ```text
    NOT agent: Linux
   ```

2. ```text
    geo.src: NL
   ```

3. ```text
    memory: *
   ```

4. ```text
    geo.src: IN and geo.dest:JP
   ```

   or

   ```text
    geo.srcdest : "IN:JP"
    ```

## PPL Exercise Solutions

1. ```sql
    source = opensearch_dashboards_sample_data_ecommerce
    | stats avg( taxful_total_price ) by customer_gender 
   ```

2. ```sql
   search source=opensearch_dashboards_sample_data_ecommerce
    | stats count() as cnt by manufacturer
    | sort -cnt
   ```

3. ```sql
   search source=opensearch_dashboards_sample_data_ecommerce
   | stats count() , sum( taxful_total_price ) , avg( taxful_total_price ) , max( taxful_total_price ) by category
   ```
