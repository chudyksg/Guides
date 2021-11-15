### Business Object Semantics
The below enables transaction processing with draft. To be implemented on the header interface CDS view
```
@ObjectModel: {

    -- Annotations for transactional processing
    semanticKey: 'ServiceEntrySheet',
    compositionRoot: true,
    transactionalProcessingEnabled: true,
    createEnabled: true,
    deleteEnabled: true,
    updateEnabled: true,

    -- Additional annotations for draft enablement
    draftEnabled: true,
    writeDraftPersistence: '/ABSOFT/SES_D',

    -- Additional ETag annotation (time stamp)
    entityChangeStateId: 'LastChangedDate'
}
```
The below annotations should be added to the consumption header view
```
@Metadata.allowExtensions: true
    
@ObjectModel: {
    
    -- Annotations for transactional processing
    semanticKey: 'ServiceEntrySheet',
    compositionRoot: true,  
    transactionalProcessingDelegated: true, 
    createEnabled: true,
    deleteEnabled: true,
    updateEnabled: true,
    
    -- Additional annotation for draft enablement    
    draftEnabled: true   
    
}
```
### Header CDS to Item CDS composition annotation
```
@ObjectModel.association.type: [#TO_COMPOSITION_CHILD]
      _ServEntrySheetItem
```
### Item CDS to Header CDS composition annotation
```
@ObjectModel.association.type: [#TO_COMPOSITION_PARENT, #TO_COMPOSITION_ROOT]
_ServiceEntrySheet,
```
