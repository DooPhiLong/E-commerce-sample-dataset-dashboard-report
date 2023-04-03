# Data mining and cleaning
## 🔨 Tool : Power query (M code)
## 📌 CLEAN and TRANSFORM DATA

### 📎 Customers Dataset

- There are 4 things I would check in customers dataset:
  - The overall info 
  - There is duplicated value of primary key or not (customer_id)
  - Checking unique values of city name, State.
  - Capitalize the first letter of city name.

<details><summary> The  Overall Infomation </summary>
  
</details>
 
 <details><summary> Checking duplicated values </summary>
  
 </details>

 <details><summary> Checking unique values of State </summary>

 </details>
 
<details><summary>  Capitalize the first letter of city name  </summary>

 </details>

---
### 2️⃣ Orders Dataset

- There are 3 things I would check in Orders dataset:
  - Check Overall Info
  - Transform data type of some columns from object to datatime
  - Check Null values

<details><summary> The  Overall  </summary>
  
```python
orders.head() 
```
![image](https://user-images.githubusercontent.com/101379141/202590328-96673499-1c64-4a7b-a446-84457184fddc.png)

```python
orders.info()
```
![image](https://user-images.githubusercontent.com/101379141/202590347-7419779c-917a-47c9-81c3-bc94df5c63e6.png)
  
 </details>

<details><summary> Transform Data Type  </summary>
  
```python
#Transforming the data type from object to datetime 
orders['order_purchase_timestamp'] = pd.to_datetime(orders['order_purchase_timestamp'], format = '%Y-%m-%d %H:%M:%S')
orders['order_approved_at'] = pd.to_datetime(orders['order_approved_at'], format = '%Y-%m-%d %H:%M:%S')
orders['order_delivered_carrier_date'] = pd.to_datetime(orders['order_delivered_carrier_date'], format = '%Y-%m-%d %H:%M:%S')
orders['order_delivered_customer_date'] = pd.to_datetime(orders['order_delivered_customer_date'], format = '%Y-%m-%d %H:%M:%S')
orders['order_estimated_delivery_date'] = pd.to_datetime(orders['order_estimated_delivery_date'], format = '%Y-%m-%d %H:%M:%S')

orders.info()
```
![image](https://user-images.githubusercontent.com/101379141/202590474-5722e629-b482-4c4e-8065-f1e7b2b266f6.png)
  
</details>

<details><summary> Check Null Values </summary>

```python
#Check Null Values
orders.isnull().sum()
```

```python
#Check Percent of Null values. 
# Because the null values does not accounts much of total dataset ( about 3% is max), we can ignore or drop it
# However, The null values of these columns were also mean that the orders were not delivered to customer or carrier. So We can not drop them. 
orders.isnull().mean() * 100

```
![image](https://user-images.githubusercontent.com/101379141/202590671-f64db3e4-4fa4-49d6-9c68-908cea61fee4.png)

</details>

---
### 3️⃣ Order Items Dataset

- The order items dataset is clean so we don't need to adjust it.

<details><summary> The  Overall  </summary>

 ```python
 order_items.head() 
 ```
 ![image](https://user-images.githubusercontent.com/101379141/202591464-b8cd4a4a-91f9-401c-9c75-e2c33a6235e3.png)

 ```python
 order_items.describe() 
 ```
 ![image](https://user-images.githubusercontent.com/101379141/202591488-d3e2293e-cd45-4865-ac51-c0e7d548658d.png)

 ```python
 order_items.info() 
 ```
 
 ![image](https://user-images.githubusercontent.com/101379141/202591523-23610480-51e9-401c-9ca9-3b462101b617.png)
 
  
</details>
 
---
### 4️⃣ Order Payments Dataset

- After The order payments dataset is clean. We don't need to adjust it.

<details><summary> The  Overall  </summary>

 ```python
 order_payments.head() 
 ```
![image](https://user-images.githubusercontent.com/101379141/202591939-ccd8d81a-2a52-4cab-affc-efded8b4b934.png)

```python
order_payments.info() 
```
![image](https://user-images.githubusercontent.com/101379141/202591974-428d8f50-9fd3-4ce2-b206-8dbbd40c60e1.png)

  
```python
order_payments['payment_type'].unique() 
```
![image](https://user-images.githubusercontent.com/101379141/202591995-81284279-97c3-49a2-a953-f3b0b3bab9cb.png)
  
</details>

---
### 5️⃣ Order Reviews Dataset

- There are 2 things that we are doing with this dataset:
  - The Overall
  - Transform data type from object to datetime 

<details><summary> The  Overall  </summary>

 ```python
 order_reviews.head() 
 ```
![image](https://user-images.githubusercontent.com/101379141/202593250-30d0b6e6-fd98-4413-98ac-93772b75b8d7.png)
  
```python
order_reviews.info() 
```
![image](https://user-images.githubusercontent.com/101379141/202593274-eb0ce20e-5c1e-4b96-8936-ed3a2d43536a.png)
  
```python
order_reviews['review_score'].value_counts()
```
![image](https://user-images.githubusercontent.com/101379141/202593298-38b5ceb6-5e8d-4695-93c6-8d624c479258.png)
 
</details>

<details><summary> Transform data type  </summary>

```python
 order_reviews['review_creation_date'] = pd.to_datetime(order_reviews['review_creation_date'])
order_reviews['review_answer_timestamp'] = pd.to_datetime(order_reviews['review_answer_timestamp'])

order_reviews['review_creation_date'] = order_reviews.review_creation_date.dt.strftime('%m/%d/%Y')
order_reviews['review_answer_timestamp'] = order_reviews.review_answer_timestamp.dt.strftime('%m/%d/%Y')
order_reviews.head(5)
 ```
  
![image](https://user-images.githubusercontent.com/101379141/202593442-736774bf-875a-4ff0-a273-bb31b2958a31.png)
 
</details>

---  
###  6️⃣Products Dataset
  
- There are 3 things that we are doing with this dataset:
  - The Overall
  - Checking Null values .
  - Replacing the "0 gram" of product weight to median

<details><summary> The  Overall  </summary>
  
 ```python
 products.head() 
 ```
![image](https://user-images.githubusercontent.com/101379141/202595562-89179cb5-d1b8-4503-ac9b-908cc286c44a.png)
  
```python
products.info() 
```
![image](https://user-images.githubusercontent.com/101379141/202595592-4a82a95a-9136-48ed-bba7-2fa4bc89777c.png)

  
```python
products.describe()
``` 
![image](https://user-images.githubusercontent.com/101379141/202595632-653f740c-1449-4279-a542-d9d506b269bf.png)

```python
# Min of product_weight_g = 0 , so we check this column to make sure there is nothing anomaly
products[products['product_weight_g']== 0]  
```
  
 ![image](https://user-images.githubusercontent.com/101379141/202595685-8a7e6a1c-c51d-4c21-a6b4-779cce86637b.png)

</details>

<details><summary> Check Null Values </summary>

```python
  #Check Null Values
  products.isnull().sum()
  ```
  ![image](https://user-images.githubusercontent.com/101379141/202596089-660af9b9-c2b1-4f9b-b894-945d6c388aba.png)


```python  
#Check Null values of category name column
products[products['product_category_name'].isnull() == True]
```
![image](https://user-images.githubusercontent.com/101379141/202596188-5f0c384f-8126-4b1e-b4b6-fc80c8d0841b.png)

```python
#Check Null values of weight column
products[products['product_weight_g'].isnull() == True]
```
  
![image](https://user-images.githubusercontent.com/101379141/202596235-c4e5dffb-90cf-4c80-97a0-3d14e83ba554.png)  

 ```python
  #Drop all 610 Null value rows , because they are not significant ( 610  rows compare to 32951 total entries )
  products = products.dropna()  
  products.isnull().sum()  
 ```
 ![image](https://user-images.githubusercontent.com/101379141/202596277-466fbd1b-d48b-4621-87a7-de256a357f78.png)
                                                                                       
</details>  

<details><summary> Check product weight column </summary>

  ```python
  #Check product_weight_g distribution
  sns.distplot(products['product_weight_g'])
  ```
  ![image](https://user-images.githubusercontent.com/101379141/202597280-5893fdcf-addb-40af-8b80-13b6561c8070.png)
  
  ```python
  #Replace "0" values of weight to "median"
  products['product_weight_g']= products['product_weight_g'].replace(0, products['product_weight_g'].median())  
  ```
  
  ```python
  products.describe()
  ```
  ![image](https://user-images.githubusercontent.com/101379141/202597233-2e49fc07-7420-4dad-98a2-39934266b62a.png)
  
</details>  

---  
### 7️⃣ Product Name Translation Dataset
  
- There are 3 things that we are doing with this dataset:
  - Checking The Overall  
  - Merge the product name of 2 table  
  - Checking Null values of merged table and replacing Null values by new category. 

<details><summary> The Overall </summary>

```python
product_name_translation.head()
```
![image](https://user-images.githubusercontent.com/101379141/202599864-11041880-bf87-475b-b51e-2fb433797183.png)

```python
product_name_translation.info()
```
  
![image](https://user-images.githubusercontent.com/101379141/202599948-948b1539-f4af-48cd-b166-b622589b4209.png)
  
</details>  

<details><summary> Merge product name of 2 table </summary>

```python
#Compare the product name of 2 table 
print(product_name_translation['product_category_name'].nunique())
print(products['product_category_name'].nunique()) 
```
![image](https://user-images.githubusercontent.com/101379141/202600071-0df0c1bc-816a-48df-8eef-aa62d1f147b6.png)

```python
product_summarize = products.merge(product_name_translation,how ='left', on = 'product_category_name' )  
```
  
</details>  

<details><summary> Check Null values of merged table and Replace Null values </summary>
  
```python
#Check Null values
product_summarize.isnull().sum()  
```
![image](https://user-images.githubusercontent.com/101379141/202600293-a3e49db7-04e0-4845-8eb0-f3ee59b72501.png)

```python
product_summarize[product_summarize['product_category_name_english'].isnull() == True]  
```
![image](https://user-images.githubusercontent.com/101379141/202600383-93313b22-bed2-4d2c-836b-27bf91d69c18.png)

```python
#Replace Null Value by Unspecified

product_summarize['product_category_name_english'] = product_summarize['product_category_name_english'].fillna(value ='Unspecified')  
product_summarize.isnull().sum()  

```
![image](https://user-images.githubusercontent.com/101379141/202600501-2c762e90-fa24-4e68-a958-ca4564de51c6.png)
    
</details>  

---
### ✔ Save File 

<details><summary> Code here  </summary>

```python
#File customers
customers.to_csv('/content/drive/MyDrive/Final/De 1/customers_dataset.csv',index=False)

#File orders dataset
orders.to_csv('/content/drive/MyDrive/Final/De 1/orders_dataset.csv',index=False)

#File orders items
order_items.to_csv('/content/drive/MyDrive/Final/De 1/order_items_dataset.csv',index=False)

#File order payments
order_payments.to_csv('/content/drive/MyDrive/Final/De 1/order_payments_dataset.csv',index=False)

#File order review
order_reviews.to_csv('/content/drive/MyDrive/Final/De 1/order_reviews_dataset.csv',index=False)

#Merged file of product & produc_translation 
product_summarize.to_csv('/content/drive/MyDrive/Final/De 1/product_summarize_dataset.csv',index=False)

```
</details>  

---
## 📊 POWER BI

### 1. Transform Data

After import dataset, we need to promote header of columns and change some data type columns. 

<details><summary> Customers dataset  </summary>

 - Source (first 10 rows)
  
![image](https://user-images.githubusercontent.com/101379141/202607728-04d35ccc-0db2-49b4-97f8-0d6e2cb0c03c.png)
  
 - Transformed 
  
 ![image](https://user-images.githubusercontent.com/101379141/202607690-acfd75d9-4359-4af6-85b8-c98c78fac434.png)

</details>  

<details><summary> Order Items dataset  </summary>
 
- Source (first 10 rows)
  
 ![image](https://user-images.githubusercontent.com/101379141/202607942-2038f7a4-e235-4a46-ac7b-86e2b673b294.png)
  
- Transformed
  
 ![image](https://user-images.githubusercontent.com/101379141/202608029-b7bc5871-cca9-477f-a03b-773566b168aa.png)
  
</details>  


<details><summary> Order Payments dataset  </summary>

- Source (First 10 rows)
  ![image](https://user-images.githubusercontent.com/101379141/202608207-1e51c2b0-5257-458c-8560-acbe82bdc4ec.png)
  
- Transformed
  ![image](https://user-images.githubusercontent.com/101379141/202608270-29d59313-6861-4c00-a2e1-643fc7f92ccd.png)
</details>  

<details><summary> Order Reviews dataset  </summary>

- Source (First 10 rows)
![image](https://user-images.githubusercontent.com/101379141/202608439-6de93b9f-57e5-4dde-8baf-46037492f1d8.png)

- Transformed
![image](https://user-images.githubusercontent.com/101379141/202608488-a2aa5431-19b6-4203-bf35-3515ab38ebdf.png)

</details>  

<details><summary> Orders dataset  </summary>

- Source (First 10 rows)
 ![image](https://user-images.githubusercontent.com/101379141/202608610-952075c6-cc13-4447-af29-f3a0d6ca5d7d.png)
  
- Transformed
  ![image](https://user-images.githubusercontent.com/101379141/202608652-21c233c4-5298-4060-a50b-043992d4cfdd.png)

</details>  

<details><summary> Product Summarize Dataset  </summary>
  
- Source (First 10 rows)
![image](https://user-images.githubusercontent.com/101379141/202608743-b762ec37-e78f-4db7-ba56-fc6e6d2fd238.png)

- Transformed  
![image](https://user-images.githubusercontent.com/101379141/202608775-130d0dd2-b3ec-4063-9eb1-174b5270b585.png)

</details>  

### 2. Dax, Measure

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

### 3. Create New Table

To match the average score of order. I have to create new table 

```
Average = SUMMARIZECOLUMNS(order_reviews_dataset[order_id],"Average_Score",AVERAGE(order_reviews_dataset[review_score]))
```
<details><summary> The First Few Rows  </summary>
 
![image](https://user-images.githubusercontent.com/101379141/202612783-d8974939-f0b0-43e3-a655-f003e98c0758.png)
  
</details>

**Final Model**

<details><summary> Click Here  </summary>

![image](https://user-images.githubusercontent.com/101379141/202614575-3ffb8db6-9e53-42af-8a08-99f5423c4a5e.png)

</details>
