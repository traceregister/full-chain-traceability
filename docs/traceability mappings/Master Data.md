# Master Data
Master Data can be defined using the Traceability Mappings such as Trade Items, SCEs, Trading Parties and Fishing Areas.

## Trade Items / Product Definitions
It is possible the Trade Items or Product Definitions created using the Traceability Mappings

The following KDEs are available:
* **GTIN**
* **Item Code** *(required)*
* **Scientific Name**
* **Short Description** *(required)*
* **Product Form Category**

### Example XML
```
<TradeItem ItemCode="{XPath=DataTable/ItemCode}" GTIN="{XPath=DataTable/GTIN}">
	<ShortDescription>{XPath=DataTable/CommonName}</ShortDescription>
	<ScientificName>{XPath=DataTable/ScientificName}</ScientificName>
	<ProductFormCategory>Whole</ProductFormCategory>
</TradeItem>
```
## Supply Chain Entities 
It is possible to define Supply Chain Entities using the Traceability Mappings.

The following KDEs are available:
* **GLN** 
* **XRef** *(required)*
* **Name** *(required)*
* **Vessel**
	* Number
	* Permit Number
	* Gross Tonnage
	* Length
	* Call Sign
	* IMO Number
	* Flag Country Code *(ISO)*
* **Landing**
* **Address**
	* Address 1
	* Address 2
	* City
	* County
	* State
	* Zip Code
	* Country ISO

### Example XML
```
<SupplyChainEntity GLN="{XPath=DataTable/GLN}" XRef="{XPath=DataTable/SCEXRef}">
	<Name>{XPath=DataTable/Name}</Name>
	<Vessel>
		<Number>{XPath=DataTable/VesselNumber}</Number>
		<IMONumber>{XPath=DataTable/IMONumber}</IMONumber>
		<CallSign>{XPath=DataTable/CallSign}</CallSign>
		<PermitNumber>{XPath=DataTable/VesselPermitNumber}</PermitNumber>
		<GrossTonnage Value="{XPath=DataTable/GrossTonnage/@Value}" UoM="{XPath=DataTable/GrossTonnage/@UoM}"></GrossTonnage>
		<Length Value="{XPath=DataTable/Length/@Value}" UoM="{XPath=DataTable/Length/@UoM}"></Length>
		<FlagCountryCode>{XPath=DataTable/FlagCountryCode}</FlagCountryCode>		
	</Vessel>
	<Landing>
		<Port>{XPath=DataTable/Port}</Port>
	</Landing>
	<Address>
		<Address1>{XPath=DataTable/Address1}</Address1>
		<Address2>{XPath=DataTable/Address2}</Address2>
		<City>{XPath=DataTable/City}</City>
		<County>{XPath=DataTable/County}</County>
		<State>{XPath=DataTable/State}</State>
		<Zip>{XPath=DataTable/Zip}</Zip>
		<CountryIso>{XPath=DataTable/CountryIso}</CountryIso>
		<Latitude>{XPath=DataTable/Latitude}</Latitude>
		<Longitude>{XPath=DataTable/Longitude}</Longitude>
	</Address>
</SupplyChainEntity>
```

## Trading Parties
It is possible to define Trading Parties using the Traceability Mappings.

The following KDEs are available:
* **PGLN** 
* **XRef** *(required)*
* **Name** *(required)*

### Example XML
```
<TradingPartner PGLN="{XPath=DataTable/PGLN}" XRef="{XPath=DataTable/XRef}">
	<Name>{XPath=DataTable/Name}</Name>
</TradingPartner
```
