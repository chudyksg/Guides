### Get elemeny by id
```Javascript
    let segBtn = {};

    if (sap.n) { //If run in launchpad
        segBtn = sap.ui.getCore().byId(sap.n.currentView.createId(segBtnId));
    } else { //If run standalone
        segBtn = sap.ui.getCore().byId(segBtnId);
    }
```
