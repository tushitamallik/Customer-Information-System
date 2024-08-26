# Customer-Information-System
The Customer Information System is an independent software system developed to create the mapping to load the target from the source file after applying all the logics that is mentioned in the mapping document System diagram.

## Objective
1. Successfully designed and implemented a data integration pipeline for customer information using Informatica PowerCenter.
2. Transformed customer data using various techniques to meet specific requirements.
3. Loaded and stored transformed data in designated databases and flat files.

## Functional Requirement
Create the mapping to load the target from the source file after applying all the logic that is mentioned in the mapping document.

## Table of Content
1. Source File
2. Target Files
3. Mapping XMLs
4. Session Logs
5. Workflow XMLs
6. Documentation

## Platform
Informatica PowerCenter

## Source 
1. SAPP_CUSTOMER
   
| FIELD_NAME    | DATA_TYPES  |
| ------------- | ----------- |
| FIRST_NAME    | STRING(40)  |
| MIDDLE_NAME   | STRING(40)  |
| LAST_NAME     | STRING(40)  |
| SSN           | STRING(9)   |
| APT_NO        | STRING(7)   |
| STREET_NAME   | STRING(30)  |
| CUST_CITY     | STRING(30)  |
| CUST_STATE    | STRING(30)  |
| CUST_COUNTRY  | STRING(30)  |
| CUST_ZIP      | STRING(7)   |
| CUST_PHONE    | NUMBER(10)  |
| CUST_EMAIL    | STRING(40)  |

3. SAPP_ITEM
   
| FIELD_NAME  | DATA_TYPES  |
| ----------- | ----------- |
| ITEM_CODE   | NUMBER(10)  |
| ITEM_NAME   | STRING(30)  |
| ITEM_PRICE  | NUMBER(9)   |

5. SAPP_CUST_ITEM
   
| FIELD_NAME    | DATA_TYPES  |
| ------------- | ----------- |
| FIRST_NAME    | STRING(40)  |
| MIDDLE_NAME   | STRING(40)  |
| LAST_NAME     |  STRING(40) |
| CUST_SSN      | STRING(9)   |
| ITEM_CODE     | NUMBER(10)  |
| NO_OF_ITEM    | NUMBER(5)   |

## Transformations Applied
1. For Target SAPP_D_CUSTOMER

| **Target Table/File name** |	**Target Field names**	| **Target DataType** | 	**Description** |	 **Mapping Logic** |	**Source File Name** |	**Source File Column Names** | 	**Source Data Type** |
| ------------- | ----------- | ------------- | ----------- | ------------- | ----------- | ------------- | ----------- |
|SAPP_D_CUSTOMER|	CUST_ID	|Number(10)|	Surrogate key of the customer table. Used to uniquely identify a row.	|"System generated based on Customer SSN. | - | - | - |
| SAPP_D_CUSTOMER |	CUST_F_NAME	|VARCHAR2(40)	|First Name of the Customer|	Convert the Name to Title Case	|SAPP_CUSTOMER|	FIRST_NAME|	STRING(40)|
|SAPP_D_CUSTOMER	|CUST_M_NAME|	VARCHAR2(40)|	Middle Name of the customer|	Convert the middle name in lower case	|SAPP_CUSTOMER|	MIDDLE_NAME|	STRING(40)|
|SAPP_D_CUSTOMER	|CUST_L_NAME|	VARCHAR2(40)|	Last Name of the customer	|Convert the Last Name in Title Case|SAPP_CUSTOMER|	LAST_NAME	|STRING(40)|
|SAPP_D_CUSTOMER|	CUST_SSN	NUMBER(9)|	Social Security Number of the customer (National ID)|	Direct move ( Abort the session if SSN is invalid. Convert to number )|	SAPP_CUSTOMER	|SSN|	STRING(9)|
|SAPP_D_CUSTOMER	|CUST_STREET	|VARCHAR2(38)|	Apartment no and Street name of customer's Residence|	Concatenate Apartment no and Street name of customer's Residence with comma as a seperator|	SAPP_CUSTOMER	|STREET_NAME,APT_NO	|STRING(30),String(7)|
|SAPP_D_CUSTOMER	|CUST_CITY|	VARCHAR2(30)	|Customer’s Current City	|Direct Move|	SAPP_CUSTOMER|	CUST_CITY|	STRING(30)|
|SAPP_D_CUSTOMER	|CUST_STATE	|VARCHAR2(30)|	Customer’s State code|	Direct Move|	SAPP_CUSTOMER	|CUST_STATE|	STRING(30)|
|SAPP_D_CUSTOMER|	CUST_COUNTRY|	VARCHAR2(30)|	Customer’s country code|	Direct move|	SAPP_CUSTOMER|	CUST_COUNTRY	|STRING(30)|
|SAPP_D_CUSTOMER|	CUST_ZIP|	NUMBER(7)|	Zip code of Customer's Country|	Direct move ( Convert to number )|	SAPP_CUSTOMER|	CUST_ZIP|	STRING(7)|
|SAPP_D_CUSTOMER|	CUST_PHONE|	VARCHAR2(12)|	Contact Number of the customer	|Change the format to xxx-xxx-xxxx|SAPP_CUSTOMER|	CUST_PHONE	|NUMBER(10)|
|SAPP_D_CUSTOMER|	CUST_EMAIL|	VARCHAR2(40)|	Email address of the customer	|Direct move	|SAPP_CUSTOMER|	CUST_EMAIL	|STRING(40)|

2. For Target SAPP_D_ITEM

| **Target Table/File name** |	**Target Field names**	| **Target DataType** | 	**Description** |	 **Mapping Logic** |	**Source File Name** |	**Source File Column Names** | 	**Source Data Type** |
| ------------- | ----------- | ------------- | ----------- | ------------- | ----------- | ------------- | ----------- |
|SAPP_D_ITEM|	ITEM_CODE|	NUMBER(10)|	 Used to uniquely identify a ITEM.|	DIRECT MOVE|	SAPP_ITEM|	ITEM_CODE|	NUMBER(10)|
|SAPP_D_ITEM|	ITEM_NAME|	STRING(30)|	 Name of the ITEM|	DIRECT MOVE	| SAPP_ITEM	|ITEM_NAME|	STRING(30)|
|SAPP_D_ITEM|	ITEM_PRICE|	NUMBER(9)|	Price of ITEM|	DIRECT MOVE	 |SAPP_ITEM |ITEM_PRICE	|NUMBER(9)|

3. For Target SAPP_D_CUST_ITEM

| **Target Table/File name** |	**Target Field names**	| **Target DataType** | 	**Description** |	 **Mapping Logic** |	**Source File Name** |	**Source File Column Names** | 	**Source Data Type** |
| ------------- | ----------- | ------------- | ----------- | ------------- | ----------- | ------------- | ----------- |
|SAPP_D_CUST_ITEM|	CUST_SSN|	NUMBER(9)|	Social Security Number of the customer (National ID)|	Direct move |	SAPP_CUST_ITEM|	SSN	|STRING(9)|
|SAPP_D_CUST_ITEM	|CUST_ID	|Number(10)	|Surrogate key of the customer table. Used to uniquely identify a row.	|Lookup from Customer table acording to cust_SSN	| -|	-|	-|
|SAPP_D_CUST_ITEM	|ITEM_CODE|	NUMBER(10)|	 Used to uniquely identify a ITEM.|	DIRECT MOVE	|SAPP_CUST_ITEM|	ITEM_CODE|	NUMBER(10)|
|SAPP_D_CUST_ITEM	|ITEM_NAME|	STRING(30)|	 Name of the ITEM	|Lookup from ITEM table acording to ITEM_CODE	| -	| -	| -|
|SAPP_D_CUST_ITEM	|ITEM_PRICE|	NUMBER(9)|	Price OF ITEM	|Lookup from ITEM table acording to ITEM_CODE	| -	| -	 |-|
|SAPP_D_CUST_ITEM	|NO_OF_ITEM	|NUMBER(5)|	No of item for each customer 	|Direct Move|SAPP_CUST_ITEM |	NO_OF_ITEM|	NUMBER(5)|
|SAPP_D_CUST_ITEM	|Total_price|	Number(20)|	Total price of items for each customer have	|no_of_item*itemPrice|	 -	| -	| -|
