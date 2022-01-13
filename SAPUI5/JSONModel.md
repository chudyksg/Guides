### Create JSON Model
```
var data = {
    EDIT_MODE: false,
};
var oModel = new sap.ui.model.json.JSONModel(data);
sap.ui.getCore().setModel(oModel, 'MODE'); // Set on global level
```
