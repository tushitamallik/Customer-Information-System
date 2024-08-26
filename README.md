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

| **Target Table/File name** |	**Target Field names**	| **Target DataType** | 	**Description** |	 **Mapping Logic** |	**Source File Name** |	**Source File Column Names** | 	**Source Data Type** |
| ------------- | ----------- | ------------- | ----------- | ------------- | ----------- | ------------- | ----------- |
