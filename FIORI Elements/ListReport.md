### Header Information
```
@UI: {
    headerInfo: {
        typeName: 'Travel',
        typeNamePlural: 'Travels'
    },
    presentationVariant: [{
        sortOrder: [{
            by: 'LocalLastChangedAt',             --Initial table sorting
            direction: #DESC
        }],
        visualizations: [{
            type: #AS_LINEITEM                    --Applies to list report table
        }]
    }]
}
```
### Semantic Key
Field appears in BOLD in the table 
Has to be specified in CDS view - used for bookmarking and navigation
```
@ObjectModel.semanticKey: ['TravelID']
```
### Table Line Item
Appears as column in table
```
@UI.lineItem: [{ position: 10 }]
TravelID;
```
### Table Column Label
```
@EndUserText.label: 'Status'
OverallStatus,
```
### Table Field - Key Value Description
Object Model has to be added in the CDS view
```
@ObjectModel.text.element: ['AgencyName']
AgencyID,
_Agency.Name as AgencyName,
```
### Table Field - Show Description Only
```
@UI.lineItem: [{ position: 80 }]
@UI.textArrangement: #TEXT_ONLY //Omits the key
OverallStatus;
```
### Table Field - Criticiality
```
@UI.lineItem: [{ position: 80, criticality: 'OverallStatusCriticality' }]
@UI.textArrangement: #TEXT_ONLY
OverallStatus;
```
### Table Field - Picture
```
@UI.lineItem: [ { position: 05, label: ' ', value: '_Carrier.AirlinePicURL' } ]
_Carrier;

--The below semantic annotation in the CDS
@Semantics.imageUrl: true
Airline.carrier_pic_url as AirlinePicURL,
```    
### Filter Bar - Selection Field
```
@UI.selectionField: [{ position: 10 }]
AgencyID;
```
### Value Help
```
@Consumption.valueHelpDefinition: [{ entity : {name: '/DMO/I_Customer', element: 'CustomerID'  } }]
CustomerID,
```

### Value Help through association
```
@Consumption.valueHelp: '_ServiceOrderTypeVH'
ServiceOrderType,
```      

### Value Help - Additional Bindings
```
      @Consumption.valueHelpDefinition: [ {
        entity: {
          name: 'zi_fe_flig_000013',
          element: 'ConnectionID'
        },
        additionalBinding: [ {
          localElement: 'FlightDate',
          element: 'FlightDate'
        }, {
          localElement: 'CarrierID',
          element: 'AirlineID'
        }, {
          localElement: 'FlightPrice',
          element: 'Price'
        }, {
          localElement: 'CurrencyCode',
          element: 'CurrencyCode'
        } ]
      } ]
      ConnectionID,
 ```
### Drop Down menu fo Value Help
```
Add this in the CDS views that is used for Value Help
@ObjectModel.resultSet.sizeCategory: #XS 
```

### Defining Text Elements
-Through text association
```
@Consumption.valueHelp: '_ServiceOrderTypeVH'
ServiceOrderType,
```
-Text Elements in the Same Entity
```
@ObjectModel.text.element: ['SupplierName']
Supplier,
SupplierName,
```

### Read only
```
@ObjectModel.readOnly: true
```

### Mandatory
```
@ObjectModel.mandatory: true
```

### Searchable fields
```
@Search.searchable: true //at the top of the CDS view

 @Search.defaultSearchElement: true
 @Search.fuzzinessThreshold : 0.7
 key _PurchaseOrderItem.PurchaseOrder
```

