### Header Information
```
@UI: {
    headerInfo: {
        typeName: 'Travel',
        typeNamePlural: 'Travels'
    },
    presentationVariant: [{
        sortOrder: [{
            by: 'LocalLastChangedAt',   //Sorting of table 
            direction: #DESC
        }],
        visualizations: [{
            type: #AS_LINEITEM          //Applies to list report table
        }]
    }]
}
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

### Table Field Description
```
@ObjectModel.text.element: ['AgencyName']
AgencyID,
_Agency.Name as AgencyName,
```

### Filter Bar - Selection Field
```
@UI.selectionField: [{ position: 10 }]
AgencyID;
```
