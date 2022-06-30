### Navigation on press
```javascript
onPress: function (oEvent){
            var oItem = oEvent.getSource();
            var oCtx = oItem.getBindingContext();
            var sCarrid = oCtx.getProperty("carrid");
	this.getRouter().navTo("flights", {carrierId: sCarrid}, false);
}
```

### Wrap Mesage Box in a promise
```javascript
discardChangesConfirm: function() {
    return new Promise(function(fnResolve, fnReject) {
        jQuery.sap.require("sap.m.MessageBox");
        sap.m.MessageBox.warning("Data has been changed. Do you want to discard changes and continue without saving?", {
            title: "Warning",
            actions: ["Yes", "No"],
            onClose: fnResolve
        });
    });
}
//Then call it like this    
discardChangesConfirm().then(
    function(sAction) {
     //Resolve Function
    if (sAction === "Yes"){
    }
       
    },
    function() {
        //Reject function
    }
);
```    
