# Critical Tracking Events (CTEs)
The Traceability Mapping XML file will contain a section called `<CTEs>` at the XPath `MultiMap/Traceability/CTEs`. This will contain one or more definitions of Critical Tracking Events that are created for each row in the spreadsheet data.

Allowed CTE Types:

* CreateEvent
* HatchingEvent
* FishingEvent
* TransShipmentEvent
* OffloadEvent
* ReceiveEvent
* ShipEvent
* TransactionEvent
* MoveEvent
* FarmHarvestEvent
* ProcessingEvent
* PackagingEvent
* CommingleEvent
* MasterLotEvent

## Key
The `Key` on an event is critical in determining if an event defined on one row 
in the spreadsheet data is the same as another event on another row.

Although, each situation can warrant a different key pattern, below are some recommendations for places to start.

### Fishing, TransShipment, Offload Key Recommendations
For FishingEvent, TransShipment, and OffloadEvent, it is recommended that the key be composed of Location + Event Time. 

Some examples of this could be:
* `Key="{XPathFormat={0}-{1},DataTable/Vessel,DataTable/CatchDate}"` 
* `Key="{XPathFormat={0}-{1},DataTable/TransshipmentVessel,DataTable/TransshipmentDate}"`
* `Key="{XPathFormat={0}-{1},DataTable/Port,DataTable/OffloadDate}" `

### Hatching, Create Event Key Recommendations
For Hatching and Create events, it is recommended that the key composed of Location + Event Time + Lot Number.

Some examples of this could be:
* `Key="{XPathFormat={0}-{1}-{2},DataTable/Hatchery,DataTable,HatchingDate,DataTable/HatchLot}"`
* `Key="{XPathFormat={0}-{1}-{2},DataTable/LocationXRef,DataTable,CreateDate,DataTable/CreateLot}"`

### Receive, Ship, Move, Transaction Key Recommendations
For Receive, Ship, Move, and Transaction events, it is recommended that they is composed of Location + Event Time + (GTIN/ItemCode) + Lot Number.

Some examples of this could be:
* `Key="{XPathFormat={0}-{1}-{2},DataTable/ReceiveDate,DataTable/ItemCode,DataTable/LotNumber}"`

### Farm Harvest, Processing, Commingle, Packaging, Master Lotting Key Recommednations
For Farm Harvest, Ship, Move, Commingle, Packaging, and Master Lotting events. It is recommended that the Event Time + Output GTIN/ItemCode + Output Lot Number are used as the key.

Some examples of this include:
* `Key="{XPathFormat={0}-{1}-{2},DataTable/ProcessingDate,DataTable/OutputItemCode,DataTable/OutputLotNumber}"`
* `Key="{XPathFormat={0}-{1}-{2},DataTable/HarvestDate,DataTable/HarvestItemCode,DataTable/HarvestLotNumber}"`

## Event Time
The Event Time sets the time that the CTE took place. It has the following KDEs:
* **LocalTime** *(required)*
* **LocalTimeOffSet** *(required)*
* **TimeDelay** - This adds the specified number of hours to the LocalTime. This can be either a positive or negative integer.
* **TimeDelayHours** - This adds the specified number of hours to the LocalTime. This can be either a positive or negative integer.
* **TimeDelayDays** - This adds the specified number of days to the LocalTime. This can be either a positive or negative integer.

## Business Transaction
The Business Transaction on a CTE allows you indicate a change of ownership took place.

You have the following KDEs available for specifying the Buyer:
* **Buyer** - The Name of the Trading Partner that is the Buyer.
* **BuyerPGLN** - The PGLN of the Trading Partner that is the Buyer.
* **BuyerXRef** - The XRef of the Trading Partner that is the Buyer.
* **BuyerSCEXRef** - You can specify the XRef of an SCE, and the Buyer is set to the Owner of that SCE.

You have the following KDEs available for specifying the Seller:
* **Seller** - The Name of the Trading Partner that is the Seller.
* **SellerPGLN** - The PGLN of the Trading Partner that is the Seller.
* **SellerXRef** - The XRef of the Trading Partner that is the Seller.
* **SellerSCEXRef** - You can specify the XRef of an SCE, and the Selleris set to the Owner of that SCE.

***It is required that one Seller KDE and one Buyer KDE is specified for all Business Transactions.***



## Product Owner and Data Owner
You can reference a Product Owner or Data Owner using a PGLN or a XRef. It is recommended to use the XRef rather than a PGLN.

For referencing a Product Owner or Data Owner with XRef, you can do something like this:

```
<DataOwner>
	<XRef>{XPath=DataTable/ProcessorXRef}</XRef>
</DataOwner
<ProductOwner>
	<XRef>{XPath=DataTable/ProcessorXRef}</XRef>
</ProductOwner
```

For reference a Product owner or Data Owner with a PGLN, you can do something like this:
```
<DataOwner>
	<PGLN>0860003130308</PGLN>
</DataOwner
<ProductOwner>
	<PGLN>{XPath=DataTable/ProcessorPGLN}</PGLN>
</ProductOwner
```
***If either the Product Owner or Data Owner is not specified, then it is set to the account importing the data.***

## Object Event
Object events are events that include a list of products references. These events can create products like Fishing and Create, or they can merely record things that happen to existing product instances like Receive, Ship, Move, or Transaction.

An Object event contains the following KDEs:
* **Data Owner**
* **Product Owner**
* **Event Time** *(required)*
* **Event Location** *(required)*
* **Business Transaction**
* **Latitude**
* **Longitude**
* **Products** *(required)*
* **Contact**
* **Attachments**

***It is important that the KDEs are listed in this exact order.***

An Object event contains the following attributes:
* **Key** *(required)*
* **SumWeights** 

### Example XML
```
<ReceiveEvent Key="{XPathFormat={0}-{1}-{2}-{3},DataTable/HarvestDate,DataTable/HarvestItemCode,DataTable/HarvestLot,DataTable/FarmName}" AffectsInventory="true">
	<DataOwner>
		<PGLN>urn:gdst:traceregister.com:party:tr28401.0</PGLN>	
	</DataOwner>
	<ProductOwner>
		<PGLN>urn:gdst:traceregister.com:party:tr28401.0</PGLN>
	</ProductOwner>
	<EventTime LocalTime="{XPath=DataTable/HarvestDate}" LocalTimeOffset="-5" TimeDelay="7" />
	<EventLocation>
		<LocationXREF>{XPath=DataTable/ProcessorName}</LocationXREF>
	</EventLocation>
	<BusinessTransaction BuyerPGLN="urn:gdst:traceregister.com:party:tr28401.0"  SellerXRef="Farm Owner" />
	<Products>
		<Product ItemCode="{XPath=DataTable/HarvestItemCode}"  Lot="{XPathFormat={0}-{1}, DataTable/HarvestLot, DataTable/FarmName}" Weight="{XPath=DataTable/HarvestWeight/@Value}" UoM="KGM" />
	</Products>
</ReceiveEvent>
```

## Transformation Event
Transformation events include Commingling, Packaging, Master Lotting, Processing, and Farm Harvest events. They are defined as events that have inputs and outputs.

A Transformation event contains the following KDEs:
* **Data Owner**
* **Product Owner**
* **Event Time** *(required)*
* **Event Location** *(required)*
* **Business Transaction**
* **Latitude**
* **Longitude**
* **InputProducts** *(required)*
* **OutputProducts** *(required)*
* **Contact**
* **Attachments**

An Object event contains the following attributes:
* **Key** *(required)*
* **SumOutputWeights** 

### Example XML
```
<ProcessingEvent Key="{XPathFormat={0}-{1},DataTable/PLANTX-REF,DataTable/OutPutLotNumber}" AffectsInventory="true">
	<ProductOwner>
		<SCEXRef>{XPath=DataTable/PLANTX-REF}</SCEXRef>
	</ProductOwner>
	<EventTime LocalTime="{XPath=DataTable/DateCreated}" LocalTimeOffset="6" />
	<EventLocation>
		<LocationXREF>{XPath=DataTable/PLANTX-REF}</LocationXREF>
	</EventLocation>
	<InputProducts>
		<Product ItemCode="{XPath=DataTable/ItemConsumed}" Lot="{XPath=DataTable/InputSerialLot}" Weight="{XPath=DataTable/InputQtyLbs}"  UoM="LBR" />
	</InputProducts>
	<OutputProducts>
		<Product ItemCode="{XPath=DataTable/ItemCreated}" Lot="{XPath=DataTable/OutPutLotNumber}" Weight="{XPath=DataTable/QtyCreatedLbs}"  UoM="LBR" />
	</OutputProducts>
</ProcessingEvent>
```
