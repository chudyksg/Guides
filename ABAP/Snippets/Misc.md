### Define types with existing structure
```
  TYPES: BEGIN OF ty_form_header.
            INCLUDE TYPE zrecord_sheet_hd.
    TYPES:        search TYPE string.
    TYPES: END OF ty_form_header.
```
