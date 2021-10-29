### Header Info
```
@UI: {
    headerInfo: {
        typeName: 'Travel',
        typeNamePlural: 'Travels',
        title: {
            type: #STANDARD, value: 'Description' --Title on object page header
        },
        description: {
            value: 'TravelID'  --Description on object page header
        }
    },
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
