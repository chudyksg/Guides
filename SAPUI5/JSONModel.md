### Create JSON Model
```
var data = {
    EDIT_MODE: false,
};
var oModel = new sap.ui.model.json.JSONModel(data);
sap.ui.getCore().setModel(oModel, 'AppState'); // Set on global level
```

### Bind named JSON Model
```
{AppState>/EDIT_MODE}
```

### Change model property
```javasacript
var oModel = sap.ui.getCore().getModel("AppState");
if (oModel.getProperty("/EDIT_MODE")) {
    oModel.setProperty("/EDIT_MODE", false);
} else {
    oModel.setProperty("/EDIT_MODE", true);
}
```
