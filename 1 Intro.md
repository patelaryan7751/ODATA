## ODATA

It's a collection of restful API which allows ``webSQL``

![image](https://github.com/patelaryan7751/ODATA/assets/59426397/f3ed3240-8874-4150-aebe-66e9b91d4d5b)


2 parts of Odata are essential 
- Format: Defines how data is described, how it is serialized
- Protocol: Defines how that data is manipulated

![image](https://github.com/patelaryan7751/ODATA/assets/59426397/7a6d2770-b4c3-4f14-aa5b-c23c01cdc001)
 
![image](https://github.com/patelaryan7751/ODATA/assets/59426397/acc630d8-3919-4b24-b59d-9c7b566c5c85)

![image](https://github.com/patelaryan7751/ODATA/assets/59426397/18944bc3-a6db-441a-a3a7-ae7c7125659e)

![image](https://github.com/patelaryan7751/ODATA/assets/59426397/771761d1-9b08-4b92-8371-9645a2f06dbb)

![image](https://github.com/patelaryan7751/ODATA/assets/59426397/2e01c0f5-e001-4602-913f-84a061ea77c9)

https://services.odata.org/v2/northwind/northwind.svc/

```
<collection href="Categories">
<atom:title>Categories</atom:title>
</collection>
```

The above is the service document that contains entities to get more info on entities we can use ``$metadata``

https://services.odata.org/v2/northwind/northwind.svc/$metadata

![image](https://github.com/patelaryan7751/ODATA/assets/59426397/95506f07-d4d4-49c4-9675-3345d2063dab)

There are 2 schemas
- ``Namespace="NorthwindModel"``
-  ``Namespace="ODataWeb.Northwind.Model"``

## ``Namespace="NorthwindModel"`` schema contains

**Format**
```
<EntityType Name="Summary_of_Sales_by_Year">
<Key>
<PropertyRef Name="OrderID"/>
</Key>
<Property Name="ShippedDate" Type="Edm.DateTime" Nullable="true"/>
<Property Name="OrderID" Type="Edm.Int32" Nullable="false"/>
<Property Name="Subtotal" Type="Edm.Decimal" Nullable="true" Precision="19" Scale="4"/>
</EntityType>
<Association Name="FK_Products_Categories">
<End Role="Categories" Type="NorthwindModel.Category" Multiplicity="0..1"/>
<End Role="Products" Type="NorthwindModel.Product" Multiplicity="*"/>
<ReferentialConstraint>
<Principal Role="Categories">
<PropertyRef Name="CategoryID"/>
</Principal>
<Dependent Role="Products">
<PropertyRef Name="CategoryID"/>
</Dependent>
</ReferentialConstraint>
</Association>
```

- EntityType

```
<EntityType Name="Category">
<Key>
<PropertyRef Name="CategoryID"/>
</Key>
<Property xmlns:p8="http://schemas.microsoft.com/ado/2009/02/edm/annotation" Name="CategoryID" Type="Edm.Int32" Nullable="false" p8:StoreGeneratedPattern="Identity"/>
<Property Name="CategoryName" Type="Edm.String" Nullable="false" MaxLength="15" Unicode="true" FixedLength="false"/>
<Property Name="Description" Type="Edm.String" Nullable="true" MaxLength="Max" Unicode="true" FixedLength="false"/>
<Property Name="Picture" Type="Edm.Binary" Nullable="true" MaxLength="Max" FixedLength="false"/>
<NavigationProperty Name="Products" Relationship="NorthwindModel.FK_Products_Categories" FromRole="Categories" ToRole="Products"/>
</EntityType>
```

- Association

```
<Association Name="FK_Products_Categories">
<End Role="Categories" Type="NorthwindModel.Category" Multiplicity="0..1"/>
<End Role="Products" Type="NorthwindModel.Product" Multiplicity="*"/>
<ReferentialConstraint>
<Principal Role="Categories">
<PropertyRef Name="CategoryID"/>
</Principal>
<Dependent Role="Products">
<PropertyRef Name="CategoryID"/>
</Dependent>
</ReferentialConstraint>
</Association>
```
So as we know each **EntityType** has ``key``,``property`` and ``navigationproperty``

- key: defines the primary key of the particular entity
- property: defines each single field with their data types
- navigationproperty: relationship between 2 entity sets such as product and category are related as foriegn key
```
<NavigationProperty Name="Products" Relationship="NorthwindModel.FK_Products_Categories" FromRole="Categories" ToRole="Products"/>
```

## ``Namespace="ODataWeb.Northwind.Model"`` schema contains

**Format**
```
<EntityContainer xmlns:p7="http://schemas.microsoft.com/ado/2009/02/edm/annotation" Name="NorthwindEntities" p7:LazyLoadingEnabled="true" m:IsDefaultEntityContainer="true">
<EntitySet Name="Categories" EntityType="NorthwindModel.Category"/>
<AssociationSet Name="FK_Products_Categories" Association="NorthwindModel.FK_Products_Categories">
<End Role="Categories" EntitySet="Categories"/>
<End Role="Products" EntitySet="Products"/>
</AssociationSet>
</EntityContainer>
```

**EntityContainer**

- EntitySet
 
```
<EntitySet Name="Categories" EntityType="NorthwindModel.Category"/>
```

- AssociationSet

```
<AssociationSet Name="FK_Products_Categories" Association="NorthwindModel.FK_Products_Categories">
<End Role="Categories" EntitySet="Categories"/>
<End Role="Products" EntitySet="Products"/>
</AssociationSet>
```
## Accessing the data inside each entity

https://services.odata.org/v2/northwind/northwind.svc/Products

When we access this we get a ``feed``  which contains a lot of ``entries`` 

**Format**
```
<feed xml:base="https://services.odata.org/V2/Northwind/Northwind.svc/" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
  <title type="text">Products</title>
  <id>https://services.odata.org/v2/northwind/northwind.svc/Products</id>
  <updated>2024-04-20T11:34:40Z</updated>
  <link rel="self" title="Products" href="Products" />
  <entry>
    <id>https://services.odata.org/V2/Northwind/Northwind.svc/Products(1)</id>
    <title type="text"></title>
    <updated>2024-04-20T11:34:40Z</updated>
    <author>
      <name />
    </author>
    <link rel="edit" title="Product" href="Products(1)" />
    <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Category" type="application/atom+xml;type=entry" title="Category" href="Products(1)/Category" />
    <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Order_Details" type="application/atom+xml;type=feed" title="Order_Details" href="Products(1)/Order_Details" />
    <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Supplier" type="application/atom+xml;type=entry" title="Supplier" href="Products(1)/Supplier" />
    <category term="NorthwindModel.Product" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
    <content type="application/xml">
      <m:properties>
        <d:ProductID m:type="Edm.Int32">1</d:ProductID>
        <d:ProductName m:type="Edm.String">Chai</d:ProductName>
        <d:SupplierID m:type="Edm.Int32">1</d:SupplierID>
        <d:CategoryID m:type="Edm.Int32">1</d:CategoryID>
        <d:QuantityPerUnit m:type="Edm.String">10 boxes x 20 bags</d:QuantityPerUnit>
        <d:UnitPrice m:type="Edm.Decimal">18.0000</d:UnitPrice>
        <d:UnitsInStock m:type="Edm.Int16">39</d:UnitsInStock>
        <d:UnitsOnOrder m:type="Edm.Int16">0</d:UnitsOnOrder>
        <d:ReorderLevel m:type="Edm.Int16">10</d:ReorderLevel>
        <d:Discontinued m:type="Edm.Boolean">false</d:Discontinued>
      </m:properties>
    </content>
  </entry>
</feed>
```

https://services.odata.org/v2/northwind/northwind.svc/Products(1)

This returns an entry with ID as 1
```
<entry xml:base="https://services.odata.org/V2/Northwind/Northwind.svc/" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
  <id>https://services.odata.org/V2/Northwind/Northwind.svc/Products(1)</id>
  <title type="text"></title>
  <updated>2024-04-20T11:29:47Z</updated>
  <author>
    <name />
  </author>
  <link rel="edit" title="Product" href="Products(1)" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Category" type="application/atom+xml;type=entry" title="Category" href="Products(1)/Category" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Order_Details" type="application/atom+xml;type=feed" title="Order_Details" href="Products(1)/Order_Details" />
  <link rel="http://schemas.microsoft.com/ado/2007/08/dataservices/related/Supplier" type="application/atom+xml;type=entry" title="Supplier" href="Products(1)/Supplier" />
  <category term="NorthwindModel.Product" scheme="http://schemas.microsoft.com/ado/2007/08/dataservices/scheme" />
  <content type="application/xml">
    <m:properties>
      <d:ProductID m:type="Edm.Int32">1</d:ProductID>
      <d:ProductName m:type="Edm.String">Chai</d:ProductName>
      <d:SupplierID m:type="Edm.Int32">1</d:SupplierID>
      <d:CategoryID m:type="Edm.Int32">1</d:CategoryID>
      <d:QuantityPerUnit m:type="Edm.String">10 boxes x 20 bags</d:QuantityPerUnit>
      <d:UnitPrice m:type="Edm.Decimal">18.0000</d:UnitPrice>
      <d:UnitsInStock m:type="Edm.Int16">39</d:UnitsInStock>
      <d:UnitsOnOrder m:type="Edm.Int16">0</d:UnitsOnOrder>
      <d:ReorderLevel m:type="Edm.Int16">10</d:ReorderLevel>
      <d:Discontinued m:type="Edm.Boolean">false</d:Discontinued>
    </m:properties>
  </content>
</entry>
```

To get the data in json we can use this

https://services.odata.org/v2/northwind/northwind.svc/Products?$format=json
 

