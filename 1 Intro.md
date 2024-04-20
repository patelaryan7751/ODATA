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
EntityContainer
- EntitySet  
- AssociationSet

![image](https://github.com/patelaryan7751/ODATA/assets/59426397/a3054e81-962e-4953-b5b0-2ed85e78b1bf)
