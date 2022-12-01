---
Tags:
---
Links:

```sql
CREATE TABLE Items (
    Itemid int IDENTITY(1,1) PRIMARY KEY,
    Description varchar(255) NOT NULL,
    Price int,
    Quantity int,
    CreationDate DATETIME,
);
```

```sql
CREATE TABLE Customers (
    Customerid int IDENTITY(1,1) PRIMARY KEY,
    Name varchar(255) NOT NULL,
    Address varchar(255),
    Phone varchar(255),
    Email varchar(255),
    AmountPayable float,
    SalesLimit float,
);
```

```cs
    public int ID { get; set; }
    public string Name { get; set; }
    public string Address { get; set; }
    public string Phone { get; set; }
    public string Email { get; set; }
    public double AmountPayable { get; set; }
    public double SalesLimit { get; set; }
```


Created: 2022-11-28