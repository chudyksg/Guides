### Get elemeny by id
```Javascript
    let segBtn = {};

    if (sap.n) { //If run in launchpad
        segBtn = sap.ui.getCore().byId(sap.n.currentView.createId(segBtnId));
    } else { //If run standalone
        segBtn = sap.ui.getCore().byId(segBtnId);
    }
```

### Make function global across the launchpad
```Javascript
//Define the function
sap.ui.getCore().attachInit(function(data, navObj) {
     if (!sap.z) sap.z = {};
     if (!sap.z[localAppID]) {
         sap.z[localAppID] = {
             doUpload : function(event) {
                 console.log('doUpload: ' + localAppID);
             }
         };
     }
 });
 
 ### Pass temporary data to dialog
 ```Javascript
//Pass Data to dialog dialogObjectName.data("ParameterName", Value);
 dialogObjectName.data("ParameterName", Value);
 
 //Read Data from dialog
 let value =  dialogObjectName.data("ParameterName");
 ```

//Then call it like this
sap.z.ZUI_NAD_APP_NAME.doUpload();
```
### Expression binding
JSON Model
```
{AppState>/EDIT_MODE}
```
Table is bound - provide field name 
```
{= ${TYPE} === 'ZM01'}
```

Structure is bound - provide field name 
```
{= ${/TYPE} === 'ZM01'}
```
JSON Model based on two properties (OR)
```
{= ${AppState>/EDIT_MODE} || ${AppState>/PROCESS_MODE}  ? 'MultiSelect' : 'None' }

{= ${AppState>/EDIT_MODE} || ${AppState>/PROCESS_MODE}  }
```

