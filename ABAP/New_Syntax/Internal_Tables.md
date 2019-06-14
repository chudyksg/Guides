### Insert Into Table
```ABAP
INSERT VALUE #( col1 = 'abc' col2 = '12' col3 = 3  ) INTO TABLE itab. 
```
### Append to Table 
```ABAP
APPEND VALUE #( col1 = 'abc' col2 = '12' col3 = 3 ) TO tab1. 
```
### Check if entry exists
```ABAP
IF line_exists( my_table[ key = 'A' ] ).  
ENDIF. 
```
### Read the Table with Index
```ABAP
TRY. 
DATA(WA_MARA) = IT_MARA[ 1 ]. 
CATCH cx_sy_itab_line_not_found. 
ENDTRY. 
```

### Read the Table using  free key. 
```ABAP
TRY. 
DATA(WA_BOOKINGS) = IT_BOOKINGS[ CARRID = 'AA'  CONNID = '17'  CUSTTYPE = 'P' ].  
CATCH cx_sy_itab_line_not_found. 
ENDTRY.  
```
