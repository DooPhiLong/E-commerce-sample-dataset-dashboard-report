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

<details><summary> 1%star - to filter 1 star review  </summary>

```
%1star = divide(calculate(count(order_items_dataset[English_name_product]),order_items_dataset[Average_score] = 1),count(order_items_dataset[English_name_product]))
  
```  
</details>  

  
<details><summary> 5%star - to filter 5 star review  </summary>

```
%5star = divide(calculate(count(order_items_dataset[English_name_product]),order_items_dataset[Average_score] = 5),count(order_items_dataset[English_name_product]))
```
</details>  


<details><summary> %Comment - to calculate % order has comment   </summary>

```
%Comment = Divide(CALCULATE(count(order_reviews_dataset[Comment]), order_reviews_dataset[Comment] = "Comment"),count(order_reviews_dataset[order_id]))
```
</details> 

<details><summary> Average_Score - Average score of orders   </summary>

```
Average_Score = SUM(order_items_dataset[Average_score])/count(order_items_dataset[order_id])
```
</details>

<details><summary> Comment - Count of orders has comment   </summary>

```
Comment = CALCULATE(count(order_reviews_dataset[Comment]),order_reviews_dataset[Comment] = "Comment")
```
</details>

<details><summary> Comment_Star - Calculate review score of orders having comment   </summary>

```
Comment_Star = calculate(count(order_reviews_dataset[review_score]),order_reviews_dataset[Comment] = "Comment")
```
</details>

<details><summary> Total_time_to_delivery average per customer_city   </summary>

```
Total_time_to_delivery average per customer_city = DIVIDE(sum(orders_dataset[Total_time_to_delivery]),count(orders_dataset[order_id]))
```
</details>

<details><summary> Voucher_cat - calculate orders has applied voucher  </summary>

```
Voucher_cat = Divide(CALCULATE(count(order_payments_dataset[payment_type]),order_payments_dataset[payment_type] = "voucher"),count(order_items_dataset[product_id]))
```
</details>

<details><summary> Count Product  </summary>

```
Count_Product = COUNT(order_items_dataset[English_name_product])
```
  
</details>

<details><summary> Rank Product  </summary>

```
Rank_Product = RANKX(all(order_items_dataset[English_name_product]),[Count_Product])
```
  
</details>

## 📌 Data model

<details><summary> Click Here  </summary>

![image](https://user-images.githubusercontent.com/120476961/229851073-2f60ca70-b7ac-43af-9c37-fc629b137901.png)

</details>
