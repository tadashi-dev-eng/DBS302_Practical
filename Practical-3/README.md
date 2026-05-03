# DBS302 – Practical 3

## Theory overview

### MongoDB Data Modeling for E‑Commerce
- Data modeling in MongoDB is organization of data within a database and the links between the related entities. 

- The principle behind the data modeling in mongodb is that if we want to access the data together then we should keep it together. 


**Created Database on ecommerce and Collection.**

![alt text](./assets/step1.png)


### Insert Sample Data

**Two user document was inserted in the ecommerce database**

![alt text](./assets/step2.png)

**To confirm the two users are inserted I used the **FIND** method for more flexible queries using the collection name **users****

![alt text](./assets/step2.1.png)

**Two categories were created were the electronics is the parent and accessories is the child to store document by referencing to parent nodes to children nodes. Here the parent document stroes with parentCategoryID:null that dont have the children reference but children stores data with the parentCategoryID:electronics that points back to the parent using parentID.**

![alt text](./assets/step2.2.png)

**It confirms that the child node reference the parentCategoryId demonstrating a self referenceing relationship using the referencing pattern for hierarchical data.**

![alt text](./assets/2.2.png)

**It confirms that the parentCategoryId field references the parent category, demonstrating a self-referencing relationship using the referencing pattern for hierarchical data.**

![alt text](./assets/step2.3.png)

**Three products was inserted to demonstrate the Attribute Pattern, where variable product fields are stored in a flexible attributes map rather than fixed columns.**

![alt text](./assets/2.3.png)

**It confirms that the product has a different set of attributes keys. This flexibility is a key advantage of MongoDB's document model over rigid relational schemas.**


![alt text](./assets/step2.4.png)

**Here the orders were inserted with embedded order items and with the Key product details such as productName and unitPrice were duplicated into each item to preserve historical accuracy.**

![alt text](./assets/2.4.png)

It Confirms the following :
- Order items are embedded because they are tightly coupled with their parent order and are always read together.
- productId is still retained as a reference to allow $lookup joins when full product details are needed.
- Duplicating productName and unitPrice ensures order history remains accurate even if a product is later updated or deleted.

## Aggregation Framework: Core Analytics Queries

![alt text](./assets/q1.png)

This is a pipeline that filters paid orders, groups them by date, and computes total revenue and order count per day.

![alt text](./assets/q2.png)


![alt text](./assets/q3.png)

This is a pipeline that uses $unwind to flatten the items array and then groups by product to find the top 5 earners.


![alt text](./assets/q4.png)

I use the same pipeline with the product that uses $unwind to flatten the items array and then groups by product to find the top 5 earners.

## Query Performance Optimization

Here two seperate queries was run to retrive orders for each users by using createdAt in descending order and sort({ createdAt: -1}) is used to return the newest first in the data query.

![alt text](./assets/q5.1.png)

![alt text](./assets/q5.2.png)

The updateMany method is used to where it finds all the order and update the order status from PAID to DELIVER. 

![alt text](assets/orderstatus.png)

To confirm the updataMany method worked, Used the find() method and it shows both order shows DELIVER. All other fields are unchanged.

![alt text](assets/status1.png)

I have added 3 new documents(Wireless Ergonomic Mouse, Ultrabook Laptop 14, 27" 4K Monito) into the collection using insertMany() method.

![alt text](assets/addedp.png)

I wanted to follow a suddent pipeline : 
- Captured (order management)
- Picked (Inventor yretrieval)
- Packed (Preparation)
- shippedn(Dispatch)
- Deleviered (Final receipt)
  
So i have made a logic in the database to follow the pipeline.

I used the find method to check if the pipeline is working or not without using the time range.

![alt text](assets/findorder.png)

The main task is to filter order by status and time range. For that I used the $lte ( less than equal to) and $gte (greater than equal to)

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


Search products by text (name, description, tags).

![alt text](assets/Search_products.png)

index for order and product

![alt text](assets/index.png)


Using explain() to Analyze Query Plans

Example: Before and After Index

Run a Query Without an Index



Aggregation with Index‑Friendly 

![alt text](assets/aggregation.png)



# Referrence


- [Reference 1](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.mongodb.com/docs/manual/tutorial/model-tree-structures-with-parent-references/&ved=2ahUKEwj8892IlIyUAxW-RmwGHYBgHPwQFnoECBgQAQ&usg=AOvVaw3Nkk06LUuMscdM5R8exK67)
- [Reference 2](https://www.mongodb.com/docs/manual/reference/mql/query-predicates/comparison/)
- [Reference 3](https://www.mongodb.com/docs/manual/core/timeseries/timeseries-querying/)
- [Reference 4](https://www.mongodb.com/docs/manual/reference/method/db.collection.find/)