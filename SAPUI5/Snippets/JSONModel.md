### Create JSON Model
```javascript
var data = {
    EDIT_MODE: false,
};
var oModel = new sap.ui.model.json.JSONModel(data);
sap.ui.getCore().setModel(oModel, 'AppState'); // Set on global level
```

### Initialise named JSON Model (Existence check)
```javascript
sap.ui.getCore().attachInit(function(data, navObj) { 
    modeltabLeagues = sap.ui.getCore().getModel("FootballLeagues");
    if (!(modeltabLeagues instanceof sap.ui.model.Model)) {
        // Does not yet exist. Create it.
        modeltabLeagues = new sap.ui.model.json.JSONModel();
        sap.ui.getCore().setModel(modeltabLeagues, "FootballLeagues");        
    }
    modellistLeaguesDialog = sap.ui.getCore().getModel("FootballLeagues");
    tabLeagues.setModel( modeltabLeagues );
    listLeaguesDialog.setModel( modellistLeaguesDialog );
});
```

### Bind named JSON Model
```
{AppState>/EDIT_MODE}
```

### Change model property
```javascript
var oModel = sap.ui.getCore().getModel("AppState");
if (oModel.getProperty("/EDIT_MODE")) {
    oModel.setProperty("/EDIT_MODE", false);
} else {
    oModel.setProperty("/EDIT_MODE", true);
}
```
