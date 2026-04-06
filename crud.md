# CRUD OPERSTATION
    Create Read Update Delete
    read -> query
```
# MONGO DB
```
    building block: document
    !JSON document (BSON binary data also)
    RDBMS         |          MONGODB
    Database              database   !container for data
    Table                  collection
    Rows                   documents
    referential model          referential or embedded

```

order 
    user details + billing address + billing details
    +products selected in cart
    == order info( payment) + line items (orders, quantity)
    == {id, user_id, bill_amount, address, pay_mode, status} + 
        [{id, product_id, order_id, qty, price, amount}]
    == Referential Modeling
        orders: 
            id, user_id, bill_amount, address, paymode, status
            1, 10, 18000, xyz, gpay, pending
        order_items:
            id, product_id, order_id, qty, price, amount
            1, 1001, 1, 1, 16000, 16000
            2, 4002, 1, 2, 1000, 2000
        -----
        In mongo
            orders:
            [
                {id:1, user_id:10, bill_amount:18000, address:xyz, paymode:gpay, status:pending},
            ]

            order_items:
            [
                {id: 1, product_id:1001, order_id:1, qty:1, price:16000, amount:16000},
                {id: 2, product_id:4002, order_id:1, qty:2, price:1000, amount:2000},
            ]
    == Embedded Modelling
        orders:
            [
                {id:1, user_id:10, bill_amount:18000, address:xyz, paymode:gpay, status:pending,
                    items:[
                        {id: 1, product_id:1001, order_id:1, qty:1, price:16000, amount:16000},
                        {id: 2, product_id:4002, order_id:1, qty:2, price:1000, amount:2000},
                    ]},
            ]
            ...
        
Example: Trainer Management Platform
-db: trainer_app_db
-collections: 
    -trainers: {id, name, skills, photo}
    -admins: {id, email, password, role}


1. mobile management 
    mobiles{id, name, model, price, photo}
    admins

2. patient management
    patients{id, name, age, gender, photo}
    admins

3. cab management
    cars{id, model, number, type}
    admins


test> show databases
test> use trainer_app_db  --use is used to connect and make the db current one
trainer_app_db>show databases
trainer_app_db> db.trainers.insertOne({"name": "nithin", "skills": "javascript", "photo": ""})
trainer_app_db>show collections
trainer_app_db> db.trainers.find()
trainer_app_db> db.trainers.insertOne({"name": "Mahesh", "skills": "java", "photo": ""})
trainer_app_db> db.trainers.find({name:"mahesh"})
db.trainers.updateOne({"name": "mahesh"}, {$set:{"skills": "python"}})
trainer_app_db> db.trainers.find()


trainer_app_db> db.admins.insertMany([{"email":"jaiswal@gmail.com", "password": "1234", "role":"manager"}, {"email":"virat@gmail.com", "password":"1234", "role":"agent"}])
trainer_app_db> db.admins.find()






```