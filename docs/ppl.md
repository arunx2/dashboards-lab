## PPL
PPL is a rich and powerful unix style piped processing language where you can pipe to previous results.
You can run PPL queries either in **Query Workbench** or **Event analytics** under Observability
In this lesson, we will use the ecommerce data.

- To view all documents from an index 
    ```sql
    search source=opensearch_dashboards_sample_data_ecommerce;
    ```

- To select specific fields
    ```sql
     search source=opensearch_dashboards_sample_data_ecommerce
   | fields order_id, customer_full_name, taxful_total_price
    ```
- To rename the fields
  ```sql
    search source=opensearch_dashboards_sample_data_ecommerce 
    | where taxful_total_price > 100.00
    | rename order_id as OrderID, customer_full_name as CustomerName , taxful_total_price as OrderValue 
    | fields OrderID, CustomerName, OrderValue
  ```
  
- To select documents based on a condition
    ```sql
    search source=opensearch_dashboards_sample_data_ecommerce
   | where taxful_total_price > 100.00
   | fields order_id, customer_full_name, taxful_total_price
    ```
- To select documents based on compound conditions
  ```sql
  search source=opensearch_dashboards_sample_data_ecommerce 
  | where taxful_total_price > 100 and total_unique_products <= 2
  | fields order_id, customer_full_name, taxful_total_price
  ```
  
- deduplicate based on customer order id. In this data set, we don't have duplicates
  you can try with email. It will keep the first document by default. 
  you can have a list of fields as well.you can keep or ignore the empty 
  values by setting `keepempty=true` (Default: false). It is possible to remove
  duplicates only if they are consecutive by setting `consecutive=true` (Default: false)
  ```sql
  search source=opensearch_dashboards_sample_data_ecommerce
  | dedup order_id
  | fields order_id, customer_full_name, email, taxful_total_price, customer_gender | sort -email
   ```
- sort the results you can use `+`(Ascending by default) or `-`(descend)
  ```sql
  search source=opensearch_dashboards_sample_data_ecommerce
   | sort - taxful_total_price
   | fields order_id , customer_full_name , taxful_total_price 
  ```

- Using `stats` command to calculate the aggregation from search result.
  ```sql
  search source=opensearch_dashboards_sample_data_ecommerce 
  | stats count() , sum( taxful_total_price ) , avg( taxful_total_price ) , max( taxful_total_price )
  ```
- you can also group by a field or `span` on timestamp. In this sample, it
  return the customers order count and total sales value.
  ```sql
  source = opensearch_dashboards_sample_data_ecommerce
   | stats sum( taxful_total_price ), count() as count by customer_id
   | sort -count
  ```

Exercise:
1. find out average sales by gender
2. Find out top manufacturers based on order count
3. Find out category wise count and total sales value. 

You can find answers [here](./solutions.md)