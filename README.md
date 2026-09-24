

import numpy as np
import pandas as pd
     

df=pd.read_csv("/content/Ecommerce_Order_Test_Dataset.csv")
     

df.head()
     
Order_ID	Order_Date	Delivery_Date	Customer_Name	Gender	City	Category	Product	Payment_Mode	Quantity	Unit_Price	Discount	Rating
0	ORD0001	01-01-2025	06-01-2025	Customer_058	Male	Mumbai	Clothing	Jacket	upi	5	1470.84	0.05	4.4
1	ORD0002	02-01-2025	05-01-2025	Customer_001	Male	Delhi	Books	Data Science Guide	Debit Card	3	2114.91	0.20	3.0
2	ORD0003	04-01-2025	06-01-2025	Customer_047	male	Mumbai	Electronics	Keyboard	Cash	3	3053.63	0.20	3.3
3	ORD0004	06-01-2025	09-01-2025	Customer_034	Female	Chennai	Clothing	Sneakers	Debit Card	2	1427.69	0.00	3.6
4	ORD0005	08-01-2025	15-01-2025	Customer_032	Female	Coimbatore	Clothing	Jeans	UPI	4	752.61	0.20	3.8

df.shape
     
(101, 13)

df.columns
     
Index(['Order_ID', 'Order_Date', 'Delivery_Date', 'Customer_Name', 'Gender',
       'City', 'Category', 'Product', 'Payment_Mode', 'Quantity', 'Unit_Price',
       'Discount', 'Rating'],
      dtype='object')

df.info()
     
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 101 entries, 0 to 100
Data columns (total 13 columns):
 #   Column         Non-Null Count  Dtype  
---  ------         --------------  -----  
 0   Order_ID       101 non-null    object 
 1   Order_Date     101 non-null    object 
 2   Delivery_Date  101 non-null    object 
 3   Customer_Name  100 non-null    object 
 4   Gender         101 non-null    object 
 5   City           100 non-null    object 
 6   Category       101 non-null    object 
 7   Product        101 non-null    object 
 8   Payment_Mode   100 non-null    object 
 9   Quantity       101 non-null    int64  
 10  Unit_Price     100 non-null    float64
 11  Discount       101 non-null    float64
 12  Rating         100 non-null    float64
dtypes: float64(3), int64(1), object(9)
memory usage: 10.4+ KB

df.describe()
     
Quantity	Unit_Price	Discount	Rating
count	101.000000	100.000000	101.000000	100.000000
mean	3.168317	2579.265200	0.092079	3.738000
std	1.456498	1375.131202	0.070969	0.687813
min	1.000000	166.990000	0.000000	2.600000
25%	2.000000	1441.565000	0.050000	3.100000
50%	3.000000	2691.975000	0.100000	3.750000
75%	4.000000	3783.245000	0.150000	4.400000
max	5.000000	4927.900000	0.200000	5.000000

df.isnull().sum()
     
0
Order_ID	0
Order_Date	0
Delivery_Date	0
Customer_Name	1
Gender	0
City	1
Category	0
Product	0
Payment_Mode	1
Quantity	0
Unit_Price	1
Discount	0
Rating	1

dtype: int64

df["City"]=df["City"].fillna("Unknown")
df["Customer_Name"]=df["Customer_Name"].fillna("Unknown")
     

mean=df["Rating"].mean()
df["Rating"]=df["Rating"].fillna(mean)
     

df["Payment_Mode"]=df["Payment_Mode"].fillna("Unknown")
     

df.duplicated()
     
0
0	False
1	False
2	False
3	False
4	False
...	...
96	False
97	False
98	False
99	False
100	True
101 rows × 1 columns


dtype: bool

df.drop_duplicates()
     
Order_ID	Order_Date	Delivery_Date	Customer_Name	Gender	City	Category	Product	Payment_Mode	Quantity	Unit_Price	Discount	Rating
0	ORD0001	01-01-2025	06-01-2025	Customer_058	Male	Mumbai	Clothing	Jacket	upi	5	1470.84	0.05	4.4
1	ORD0002	02-01-2025	05-01-2025	Customer_001	Male	Delhi	Books	Data Science Guide	Debit Card	3	2114.91	0.20	3.0
2	ORD0003	04-01-2025	06-01-2025	Customer_047	male	Mumbai	Electronics	Keyboard	Cash	3	3053.63	0.20	3.3
3	ORD0004	06-01-2025	09-01-2025	Customer_034	Female	Chennai	Clothing	Sneakers	Debit Card	2	1427.69	0.00	3.6
4	ORD0005	08-01-2025	15-01-2025	Customer_032	Female	Coimbatore	Clothing	Jeans	UPI	4	752.61	0.20	3.8
...	...	...	...	...	...	...	...	...	...	...	...	...	...
95	ORD0096	22-06-2025	29-06-2025	Customer_013	Male	Coimbatore	Home	Table Lamp	UPI	5	4868.24	0.05	3.4
96	ORD0097	24-06-2025	26-06-2025	Customer_012	FEMALE	Pune	Home	Table Lamp	Cash	1	3049.48	0.10	3.0
97	ORD0098	26-06-2025	01-07-2025	Customer_031	Male	Mumbai	Books	Exam Guide	upi	4	1196.86	0.05	4.8
98	ORD0099	28-06-2025	01-07-2025	Customer_046	Female	Madurai	Home	Water Bottle	UPI	3	4126.77	0.10	4.0
99	ORD0100	30-06-2025	07-07-2025	Customer_002	FEMALE	Delhi	Electronics	Headphones	Credit Card	1	1790.90	0.20	3.5
100 rows × 13 columns


df=pd.DataFrame()
df.shape
     
(0, 0)

df["Total_Price"]=df["Quality"]*df["Unit_Price"]
df["Discount_Amount"]=df["Total_Price"]*df["Discount"]
df["Final_Amount"]=df["Total_Price"]-df["Discount_Amount"]
     
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
/usr/local/lib/python3.13/dist-packages/pandas/core/indexes/base.py in get_loc(self, key)
   3804         try:
-> 3805             return self._engine.get_loc(casted_key)
   3806         except KeyError as err:

index.pyx in pandas._libs.index.IndexEngine.get_loc()

index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()

pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()

KeyError: 'Quality'

The above exception was the direct cause of the following exception:

KeyError                                  Traceback (most recent call last)
/tmp/ipykernel_564/1210172813.py in <cell line: 0>()
----> 1 df["Total_Price"]=df["Quality"]*df["Unit_Price"]
      2 df["Discount_Amount"]=df["Total_Price"]*df["Discount"]
      3 df["Final_Amount"]=df["Total_Price"]-df["Discount_Amount"]

/usr/local/lib/python3.13/dist-packages/pandas/core/frame.py in __getitem__(self, key)
   4100             if self.columns.nlevels > 1:
   4101                 return self._getitem_multilevel(key)
-> 4102             indexer = self.columns.get_loc(key)
   4103             if is_integer(indexer):
   4104                 indexer = [indexer]

/usr/local/lib/python3.13/dist-packages/pandas/core/indexes/base.py in get_loc(self, key)
   3810             ):
   3811                 raise InvalidIndexError(key)
-> 3812             raise KeyError(key) from err
   3813         except TypeError:
   3814             # If we have a listlike key, _check_indexing_error will raise

KeyError: 'Quality'
