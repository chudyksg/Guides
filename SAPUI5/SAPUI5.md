### Navigation on press
```javascript
onPress: function (oEvent){
            var oItem = oEvent.getSource();
            var oCtx = oItem.getBindingContext();
            var sCarrid = oCtx.getProperty("carrid");
	this.getRouter().navTo("flights", {carrierId: sCarrid}, false);
}
```
