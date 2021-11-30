# Introduction
Traceability Mappings are used for mapping spreadsheet data into traceability data such as Critical Tracking Events, Product Definitions, Supply Chain Entities or Trading Parties.

## General Structure
The Traceability Mapping XML file should be structured like so:

```
<MultiMap>
	<DataMapping>
		<ScalarData>
			<!-- One or more <Data> elements. More information about this in the documentation below. -->
		</ScalarData>
		<DataRecords>
			<!-- One or more <Column> elements. More information about this in the documentation below. -->
		</DataRecords
	</DataMapping>
	<Traceability>
		<TradingPartners>
			<!-- One or more <TradingPartner>. More information about this in the documentation below. -->
		</TradingPartners>
		<SCEs>
			<!-- One or more <SCE> elements. More information about this in the documentation below. -->
		</SCEs>
		<TradeItems>
			<!-- One or more <TradeItem> elements. More information about this in the documentation below. -->
		</TradeItems>
		<CTEs>
			<!-- One or more Critical Tracking events. More information about this in the documentation below.
		</CTEs>
	</Traceability>
</MultiMap>
```
*It is is importnat to note that the elements in the XML file are requrired to come in a particular order.*

## Data References
Referencing Data in the XML Mapping is a key part of the mapping process.
### XPath
This is the simplest way to reference data from the Scalar Data or from the Data Records in the spreadsheet data.

An example of this is `{XPath=DataTable/HarvestDate}` in which the value will be replace with the `HarvestDate` value of the current row being processed in the spreadsheet data.

Another example is `{XPath=ScalarData/ProcessorPGLN}` in which the value will be replaced with the value of the Scalar Data `ProcessorPGLN`.

### XPathFormat
Next, we have the XPathFormat which allows you to combine multiple mapped values into a specific form.

Examples include:
* `{XPathFormat={0}-{1}-{2},DataTable/ProcessingDate,DataTable/OutputItemCode,DataTable/OutputLot}`
