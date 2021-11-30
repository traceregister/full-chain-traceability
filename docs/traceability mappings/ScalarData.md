# Scalar Data
Scalar data represents data that does not change from row to row in the spreadsheet data. 

## Column Attributes
There are several configurable attributes for each data column. 
* **Name** *(required)*
* **Title** *(required)*
* **Range** *(required)*
* **Type** *(required)*
* **Parameter**
* **GUIType**
* **Formats** *(required if datetime field)*

### Name
This is the name of the scalar used when referencing the scalar value in the mapping file. This name should be simple and in English TR5 terminology. 

Examples include:
* FarmName
* ProcessorName
* InputLot
* InputItemCode
* HarvestDate

### Title
This is the name of the scalar data that is used when displaying the CTE Loader GUI.

### Range
This is the Cell in the spreadsheet data where the value for the scalar data can be found. 

Example values:
* A1
* B5
* C3

## Scalar Types
There are different column types that help the system understand how to parse the spreadsheet cell value into a standardized value. 

The following column types are supported:

* **String**
* **DateTime**
* **Double**
* **Measurement**

### String Column Type
Any value is allowed in this column.

### DateTime Column Type
This column requires the value to be in a valid date and time format. However, it's recommended that the `Formats` is set to ensure that no matter which server is processing it, that the value in interpreted the same.

The `Formats` attribute should contain one or more date formats separated by a `|` as the delimiter.

#### Examples
* `dd-MM-yyyy`
* `dd-MM-yyyy|dd.MM-yyyy|dd/MM/yyyy`

#### Date Time Format Help
* **d**  = Represents the day of the month as a number from 1 through 31.    
* **dd**  = Represents the day of the month as a number from 01 through 31.    
* **ddd** = Represents the abbreviated name of the day (Mon, Tues, Wed, etc).    
* **dddd** = Represents the full name of the day (Monday, Tuesday, etc).    
* **h** = 12-hour clock hour (e.g. 4).   
* **hh** = 12-hour clock, with a leading 0 (e.g. 06)   
* **H** = 24-hour clock hour (e.g. 15)   
* **HH** = 24-hour clock hour, with a leading 0 (e.g. 22)   
* **m** = Minutes   
* **mm** = Minutes with a leading zero   
* **M** = Month number(eg.3)   
* **MM** = Month number with leading zero(eg.04)    
* **MMM** = Abbreviated Month Name (e.g. Dec)    
* **MMMM** = Full month name (e.g. December)    
* **s** = Seconds  
* **ss** = Seconds with leading zero    
* **t** = Abbreviated AM / PM (e.g. A or P)    
* **tt** = AM / PM (e.g. AM or PM   
* **y** = Year, no leading zero (e.g. 2015 would be 15)   
* **yy** = Year, leading zero (e.g. 2015 would be 015)   
* **yyy** = Year, (e.g. 2015)     
* **yyyy** =  Year, (e.g. 2015)    
* **K** = Represents the time zone information of a date and time value (e.g. +05:00)  
* **z** = With DateTime values represents the signed offset of the local operating system's time zone from Coordinated Universal Time (UTC), measured in hours. (e.g. +6)  
* **zz** = As z, but with leading zero (e.g. +06)      
* **zzz** = With DateTime values represents the signed offset of the local operating system's time zone from UTC, measured in hours and minutes. (e.g. +06:00)  

### Double Column Type
This column requires the value to be a valid number.

## GUI Types
The following GUI Types are allowed for scalar data:
* **String**
* **Double**
* **DateTime**
* **Measurement**
* **Location**
* **TradingPartner**
* **ProductDefinition**
* **TradingPartnerXRef**
* **FishingMethod**
* **RearingMethod**
* **ProcessingMethod**
* **Contact**


