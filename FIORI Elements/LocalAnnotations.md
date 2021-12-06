### Side effects
Create the determination in BOPF or RAP first, then use local annotations in SAP BAS
```
   <Annotations Target="xABSOFTxC_SERVENTRYSHEETT_CDS.xABSOFTxC_ServEntrySheetTType">
                <Annotation Term="Common.SideEffects" Qualifier="ServOrderChanged">
                    <Record>
                        <PropertyValue Property="SourceProperties">
                            <Collection>
                                <PropertyPath>ServiceOrder</PropertyPath>
                            </Collection>
                        </PropertyValue>
                        <PropertyValue Property="TargetProperties">
                            <Collection>
                                <PropertyPath>MaterialGroup</PropertyPath>
                                <PropertyPath>MaterialGroup_Text</PropertyPath>                               
                            </Collection>
                        </PropertyValue>
                    </Record>
                </Annotation>
            </Annotations>
```
