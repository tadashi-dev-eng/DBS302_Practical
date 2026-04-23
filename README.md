# DBS302 – Practical 3

### Create Database and Collection

![alt text](./assets/step1.png)

### Insert Sample Data

![alt text](./assets/step2.png)

![alt text](./assets/step2.1.png)

![alt text](./assets/step2.2.png)

![alt text](./assets/2.2.png)

![alt text](./assets/step2.3.png)

![alt text](./assets/2.3.png)

![alt text](./assets/step2.4.png)

![alt text](./assets/2.4.png)

## Aggregation Framework: Core Analytics Queries

![alt text](./assets/q1.png)

![alt text](./assets/q2.png)

![alt text](./assets/q3.png)

![alt text](./assets/q4.png)


## Query Performance Optimization

![alt text](./assets/q5.1.png)

![alt text](./assets/q5.2.png)

![alt text](assets/orderstatus.png)

![alt text](assets/status1.png)

![alt text](assets/addedp.png)

I wanted to follow a suddent pipeline : captured, picked, packed, shipped , deleviered. So i have made a logic in the database to follow the pipeline.


![alt text](assets/findorder.png)

Filter by status + time range:

![alt text](assets/statuwithtimerange.png)

to list the products by categoryID first we have to create the index first. The index is like a table of content that allows the system to locate belonging to specific category without scaning everysingle record in the table.


![alt text](assets/category.png)

Listing the product in electronics category

![alt text](assets/ece.png)

Sort by price highest first 

![alt text](assets/pricehigh.png)

Sort by newest first (createdAt)

![alt text](assets/created1.png)

![alt text](assets/created2.png)

Listing the product in accoriess category


![alt text](assets/accessories.png)

Sort by price — highest first

![alt text](assets/acchigh.png)

Sort by newest first (createdAt):

![alt text](assets/acc.png)
# DBS302_Practical
