### Deep Insert
```javascript
		onSOSave: function() {
			var oDate = new Date();
			oDate.setDate(oDate.getDate() + 7);
			var oSOData = this.getView().getModel("createCollection").getData();
			oSOData.CustomerID = this._pad(oSOData.CustomerID, 10);
			
			for(var i in oSOData.ToLineItems){
				var oLineData = oSOData.ToLineItems[i];
				oLineData.DeliveryDate = oDate;
				oLineData.ItemPosition = this._pad(oLineData.ItemPosition, 10);
			}
			
			var oModel = this.getOwnerComponent().getModel();
			oModel.create("/SalesOrderSet", oSOData, {
				success: $.proxy(this._showSOCreatedSuccess,this),
				error: this._showSOCreatedError,
				changeSetId: "CreateSO"
			});
		},
```
