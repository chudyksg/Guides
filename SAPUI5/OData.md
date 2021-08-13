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
		
		_pad: function(n, width, z) {
			z = z || '0';
			n = n + '';
			return n.length >= width ? n : new Array(width - n.length + 1).join(z) + n;
		},

		_showSOCreatedSuccess: function(oData, oResponse){
			var oResourceBundle = this.getOwnerComponent().getModel("i18n").getResourceBundle();
			var sMessage = oResourceBundle.getText("SalesOrderCreated", [oData.SalesOrderID]);
			
			MessageBox.show(sMessage, {
				icon: MessageBox.Icon.SUCCESS,
				title: oResourceBundle.getText("sucTitle"),
				actions: [MessageBox.OK],
				onClose: function(oAction){
					this.getOwnerComponent().getRouter().navTo("main", {}, true);
				}.bind(this)
			});
		},
		
		_showSOCreatedError: function(oError){
			try{
				var oMessage = JSON.parse(oError.responseText);
			MessageToast.show(oMessage.error.messae.value);
			}catch(err){
				MessageToast.show(oError.responseText);
			}
			
		}		
```
