### Get Selected Row
```
// List Get Selected Row
// Replace yourField with FieldName
var context = oEvent.oSource.getBindingContext();
// Get Single Field
var value = context.getProperty("yourField");
// Get Entire Model
var data = context.getObject();
```

### Get Selected Row Other
```
// List Get Selected Row
// Replace yourField with Field ID and yourList with correct List ID
var selectedItem = yourList.getSelectedItem();
var context = selectedItem.getBindingContext();
// Get Single Field
var value = context.getProperty("yourField");
// Get Entire Model
var data = context.getObject();
```

### Get Multi Selection
```
var itemsSelected = yourTable.getSelectedItems();
for (i=0; i<itemsSelected.length; i++){
var item = itemsSelected[i];
var context = item.getBindingContext();
var value = context.getProperty("yourField");
}
```

### Delete Item
```
var deleteItem = oEvent.getParameter("listItem");
var context = deleteItem.getBindingContext();
var value = context.getProperty("FIELD");
```
