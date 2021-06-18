### Header Information
```
@UI: {
    headerInfo: {
        typeName: 'Travel',
        typeNamePlural: 'Travels',
           title: {
            type: #STANDARD, value: 'Description' --Title on object page header
        },
        description: {
            value: 'TravelID'                     --Description on object page header
        }
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
Has to be specified in CDS view
```
@ObjectModel.semanticKey: ['TravelID']
```
### Header Facet - Data Point
```
    @UI.facet: [
      {
          id: 'TravelHeaderPrice',
          purpose: #HEADER,
          type: #DATAPOINT_REFERENCE,
          position: 10,
          targetQualifier: 'PriceData'
      },
      {
          id: 'TravelHeaderOverallStatus',
          purpose: #HEADER,
          type: #DATAPOINT_REFERENCE,
          position: 20,
          targetQualifier: 'StatusData'
       }
  ]

@UI.lineItem: [{ position: 70}]
@UI.dataPoint: { qualifier: 'PriceData', title: 'Total Price'}
TotalPrice;  

@UI.lineItem: [{ position: 80, criticality: 'OverallStatusCriticality' }]
@UI.textArrangement: #TEXT_ONLY
@UI.dataPoint: { qualifier: 'StatusData', title: 'Status', criticality: 'OverallStatusCriticality' }
OverallStatus;
```
### Standard Facet
```
  @UI.facet: [
    {
      label: 'General',
      id: 'Travel',
      type: #IDENTIFICATION_REFERENCE,
      purpose: #STANDARD,
      position: 10
    }
  ]
  
@UI.identification: [{ position: 10 }]
Description;    
```  

###  Fieldgroup Reference Facet 
```
  @UI.facet: [
    {
      id: 'Prices',
      purpose: #STANDARD,
      type: #FIELDGROUP_REFERENCE,
      label: 'Prices',
      position: 20,
      targetQualifier: 'PricesGroup'
    }
  ]
  
 @UI.fieldGroup: [ { qualifier: 'PricesGroup', position: 10} ]
 BookingFee;  
```

### Line Item Facet
```
    {
      id: 'Booking',
      purpose: #STANDARD,
      type: #LINEITEM_REFERENCE,
      label: 'Bookings',
      position: 20,
      targetElement: '_Booking'
    }

--Then line item annotations in _Booking entity
 @UI.lineItem: [ { position: 10 } ]
 BookingID;
 ```

### Collection Facet
```
  @UI.facet: [
-- Collection  
    {
      label: 'General Information',
      id: 'GeneralInfo',
      type: #COLLECTION,
      position: 10
    },
-- Standard Facet      
    {
      label: 'General',
      id: 'Travel',
      type: #IDENTIFICATION_REFERENCE,
      purpose: #STANDARD,
      parentId: 'GeneralInfo',
      position: 10
    },
-- Fieldgroup Reference Facet    
    {
      id: 'Prices',
      purpose: #STANDARD,
      type: #FIELDGROUP_REFERENCE,
      parentId: 'GeneralInfo',
      label: 'Prices',
      position: 20,
      targetQualifier: 'PricesGroup'
    }
  ]
  
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
@UI.textArrangement: #TEXT_ONLY
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

### Drop Down menu fo Value Help
```
Add this in the CDS views that is used for Value Help
@ObjectModel.resultSet.sizeCategory: #XS 
```
