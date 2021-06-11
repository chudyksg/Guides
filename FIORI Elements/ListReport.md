### Header Information
```
@UI: {
    headerInfo: {
        typeName: 'Travel',
        typeNamePlural: 'Travels'
    },
    presentationVariant: [{
        sortOrder: [{
            by: 'LocalLastChangedAt',   --Sorting of table 
            direction: #DESC
        }],
        visualizations: [{
            type: #AS_LINEITEM           --Applies to list report table
        }]
    }]
}
```
### Semantic Key
Field appears in BOLD in the table
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
