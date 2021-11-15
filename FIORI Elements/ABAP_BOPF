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
