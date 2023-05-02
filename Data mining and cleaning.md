# Data mining and cleaning
## 🔨 Tool : Power BI and Power query (M code)
## 📌 CLEAN and TRANSFORM DATA

### 📎 Customers Dataset
- There are 2 things I would check in customers dataset:
  - The overall info 
  - Capitalize the first letter of city name. 
 
<details><summary> Overall infomation </summary>
  
  - First sample 10 rows
  - Checking distinct, unique, error, empty values
![image](https://user-images.githubusercontent.com/120476961/229822424-ae6ffca5-7adc-43d6-af81-93a35f983b8a.png)
</details>

<details><summary>  Capitalize the first letter of city name  </summary>

  - Choose the customer_city column -> Transfrom -> Text column tab -> Format -> Capitalized Each Word
![image](https://user-images.githubusercontent.com/120476961/229824704-860cd078-6bd3-4d1b-b2a6-d8fdccd8b35e.png)
</details>

---
### 📎 Orders Dataset
- There are 2 things I would check in Orders Dataset:
  - The overall info 
  - Explain why keep or drop the null values
<details><summary> Overall infomation  </summary>
 
  - First sample 10 rows
  - Checking distinct, unique, error, empty values
![image](https://user-images.githubusercontent.com/120476961/229828915-98181e53-6fad-49e9-a40a-212b6a20b303.png)
  
</details>

 <details><summary> Null values  </summary>

- The null values of 3 columns ( order_approved_at, order_delivered_carrier_date, order_delivered_customer_date)  also mean that the orders were not delivered to customer or carrier. So We can not drop them. 
</details>




 
---
### 📎 Order Items Dataset
- The order items dataset is clean so we don't need to adjust it.

<details><summary> Overall infomation  </summary>

  - First sample 10 rows
  - Checking distinct, unique, error, empty values
![image](https://user-images.githubusercontent.com/120476961/229832657-6bca2e2f-c583-42ff-8ee5-7f20498de55c.png)
</details>
 
---
### 📎 Order Payments Dataset

- The Order Payments Dataset is clean so we don't need to adjust it.

<details><summary> Overall infomation  </summary>

  - First sample 10 rows
![image](https://user-images.githubusercontent.com/120476961/229833226-40881da2-20d2-4060-bf27-179d1ffd2786.png)
</details>

---
### 📎 Order Reviews Dataset

- There are 2 things I would check in Orders Dataset:
  - The overall info 
  - Explain why keep or drop the null values
<details><summary> Overall infomation  </summary>

  - First sample 10 rows
  - Checking distinct, unique, error, empty values
![image](https://user-images.githubusercontent.com/120476961/229834562-2cf0aaed-3879-4114-aae4-46c3ab6aa5aa.png)
  
</details>

<details><summary> Null values  </summary>

- The null values of 2 columns ( review_comment_title, review_comment_message) were also mean that the customer had no comment about the service and the comment review feature was not compulsory for customer. So we can not drop them .
</details>



---  
### 📎 Products Dataset
  
- There are 3 things that we are doing with this dataset:
  - The Overall info 
  - Checking the 0 value in 4 column product_weight_g, product_length_cm, product_height_cm, product_width_cm. IF it exist, Replacing it by median of it's column data 

<details><summary> Overall infomation  </summary>
  
  - First sample 10 rows
  - Checking distinct, unique, error, empty values
![image](https://user-images.githubusercontent.com/120476961/229841083-b7008ba3-9724-44a4-9697-b7f76c9af1b7.png)
![image](https://user-images.githubusercontent.com/120476961/229841187-aea1baa0-a9bf-46fa-a506-aadbce55fad9.png)

</details>

<details><summary> Checking the 0 value </summary>

- Drop down the arrow icon of each column to check all the values exist in that columns.
  
![image](https://user-images.githubusercontent.com/120476961/229843120-828e740e-fb1a-4292-b90c-ac3895f2fc9c.png)
  
- Only product_weight_g column has 0 value
  
![image](https://user-images.githubusercontent.com/120476961/229843396-1bc45962-9df1-45d7-a5ec-14ef8e6026ab.png)

</details>  

<details><summary> Replacing the "0 gram" of product weight to median</summary>

- Calculate the median of product_weight_g
  
  - Choose the product_weight_g column -> Transfrom -> Number column tab -> Statistics -> Median
  
![image](https://user-images.githubusercontent.com/120476961/229845989-c63385aa-8852-4c72-862d-394c3220789b.png)
  
  - We got the median 
  
![image](https://user-images.githubusercontent.com/120476961/229845511-aea2bfce-618e-491e-957a-620884d569ff.png)
  
- Replace 
  - Choose the product_weight_g column -> Transfrom -> Any column tab -> Replace values
  
  ![image](https://user-images.githubusercontent.com/120476961/229846571-ce9781cf-e860-49ae-8b20-c7c6bf1807d1.png)

</details> 

---

## 📌 Dax, Measure

To support for anlysis chart, We need to create following measure and dax :
<details><summary> Add Review score column to order_items_dataset (related with review_score column of order_reviews_dataset)   </summary>

```
Review score = LOOKUPVALUE(order_reviews_dataset[review_score],order_reviews_dataset[order_id],order_items_dataset[order_id])
```  
![image](https://user-images.githubusercontent.com/120476961/235682271-38865fa1-7500-4f7a-9a94-91d36af5892c.png)
</details>  

<details><summary> Add comment column to order_reviews_dataset (show that order has comment or not)  </summary>

```
Comment = if(order_reviews_dataset[review_comment_message] = BLANK(),"No comment","Comment")
  
```
![image](https://user-images.githubusercontent.com/120476961/235682673-bdce1cbb-5915-47f6-b942-58a7f3fb4c7b.png)

</details>  

<details><summary> Split month and year from order_delivered_customer_date column of orders_dataset table to two column </summary>

```
Month_delivered_customer_date = MONTH(orders_dataset[order_delivered_customer_date])
Year_delivered_customer_date = YEAR(orders_dataset[order_delivered_customer_date])
  
```
![image](https://user-images.githubusercontent.com/120476961/235683039-c8455168-34bc-48e7-8431-5dbd35b0c292.png)

</details>  

<details><summary> Split hour from order_purchase_timestamp column of orders_dataset table to a column </summary>

```
Hour purchase timestamp = HOUR(orders_dataset[order_purchase_timestamp])
  
```
![image](https://user-images.githubusercontent.com/120476961/235683105-976c879a-e44d-4ee1-8551-9daea07740a4.png)

</details>  

<details><summary> calculate the total time that each order is delivered to the customer </summary>

```
Total time to receive the goods = DATEDIFF(orders_dataset[order_purchase_timestamp],orders_dataset[order_delivered_customer_date],DAY)
  
```
![image](https://user-images.githubusercontent.com/120476961/235683172-86b4ca03-fc18-4fe7-a39b-012f8a5076a3.png)

</details>  

<details><summary> Count of Orders </summary>

```
Count of Orders = COUNT(orders_dataset[order_id])
  
```  
</details>  

  
<details><summary> Count of product </summary>

```
Count of product = count(order_items_dataset[product_id])
```
</details>  


<details><summary>  Count of comments  </summary>

```
Count of comment orders = COUNTROWS(FILTER(order_reviews_dataset,order_reviews_dataset[Comment] = "Comment"))
```
</details> 

<details><summary> Average review score   </summary>

```
Average review score = DIVIDE(SUM(order_reviews_dataset[review_score]), COUNT(order_reviews_dataset[review_score]))
```
</details>

<details><summary> Amount of orders previous month   </summary>

```
Orders_previous_month = 
CALCULATE([Count of Orders],
FILTER(ALLSELECTED(orders_dataset),
    if(max(orders_dataset[Month_delivered_customer_date]) = 1, 

        orders_dataset[Year_delivered_customer_date] = max(orders_dataset[Year_delivered_customer_date]) - 1
        &&
        orders_dataset[Month_delivered_customer_date] = 12, 

        orders_dataset[Year_delivered_customer_date] = max(orders_dataset[Year_delivered_customer_date])
        &&
        orders_dataset[Month_delivered_customer_date] = max(orders_dataset[Month_delivered_customer_date]) -1)))
```
</details>

<details><summary> Growth percentage monthly   </summary>

```
Growth percentage = DIVIDE(([Count of Orders]-[Orders_previous_month]),[Orders_previous_month])
```
</details>

<details><summary> Conditional statement to format the growth percentage  </summary>

```
Cond format growth per = IF ( [Growth percentage] < 0, 1,IF(ISBLANK([Growth percentage]),0,2))
```
</details>

<details><summary> Ranking amount of product category has sold  </summary>

```
Rank cate = RANKX(ALL(product_summarize_dataset[product_category_name_english]),[Count of product],,DESC,Dense)
```
</details>

## 📌 Data model

<details><summary> Click Here  </summary>

![image](https://user-images.githubusercontent.com/120476961/229851073-2f60ca70-b7ac-43af-9c37-fc629b137901.png)

</details>
