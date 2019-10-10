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
### Get total number of lines in a Table
```ABAP
DATA(lv_total_lines) = lines( lt_table ).
```
### Read the Table with Index
```ABAP
TRY. 
DATA(WA_MARA) = IT_MARA[ 1 ]. 
CATCH cx_sy_itab_line_not_found. 
ENDTRY. 
```

### Read the Table with key 
```ABAP
TRY. 
DATA(WA_BOOKINGS) = IT_BOOKINGS[ CARRID = 'AA'  CONNID = '17'  CUSTTYPE = 'P' ].  
CATCH cx_sy_itab_line_not_found. 
ENDTRY.  
```
### Modify table using key
```ABAP
TRY.
t_data[ TABLE_LINE = 20 ] = 10.
  CATCH cx_sy_itab_line_not_found.
ENDTRY.
```
### Initialise Table with values
```ABAP
TYPES: BEGIN OF ty_new, 
        f1 TYPE c, 
END OF ty_new, 

tty_new TYPE TABLE OF ty_new WITH EMPTY KEY. 
DATA(it_new) = VALUE tty_new( ( f1 = 'A') ( f1 = 'B') ). 
```
### Get Table's entry index
```ABAP
DATA(indx) = line_index( it_bookings[ carrid = 'AA' connid = '17'] ). 
```
### Filter Table 

* With single values
```ABAP
DATA(lt_flight_lh) = FILTER #( lt_flights_all USING KEY carrid WHERE carrid = 'LH ' ). 
```
* With table of values
```ABAP
DATA lt_flights_all TYPE STANDARD TABLE OF spfli WITH NON-UNIQUE SORTED KEY carrid COMPONENTS carrid. 
DATA lt_flight_final TYPE STANDARD TABLE OF spfli. 

SELECT * FROM spfli INTO TABLE @lt_flights_all. 

* Create a filter internal table with multiple values 
DATA filter_tab TYPE SORTED TABLE OF scarr-carrid WITH UNIQUE KEY table_line. 

filter_tab = VALUE #( ( 'AA ' ) ( 'LH ' ) ). 

* Apply filters 
lt_flight_final = FILTER #( lt_flights_all IN filter_tab WHERE carrid = table_line ). 
```
### Move certain fields using FOR LOOP
```ABAP
* Loop through and save Plant and Name only
DATA(lt_plant_name) = VALUE ltt_plant_name( FOR ls_plant IN lt_plant 
                                            WHERE ( regio EQ lv_regio )
                                                  ( plant = ls_plant-werks name = ls_plant-name1 ) ).
```                                                  

### Move corresponding
```ABAP
DATA: itab1 TYPE STANDARD TABLE OF lty_demo1, 
      itab2 TYPE STANDARD TABLE OF lty_demo2. 

itab1 = VALUE #( ( col1 = 'A' col2 = 'B' ) 
                 ( col1 = 'P' col2 = 'Q' ) 
                 ( col1 = 'N' col2 = 'P' ) ). 

itab2 = CORRESPONDING #( itab1 ). 
itab2 = CORRESPONDING #( itab1 EXCEPT COL2 ). 
itab2 = CORRESPONDING #( itab1 MAPPING COL3 = COL2 EXCEPT COL2 ). 
```
### Move corresponding keeping target lines
```ABAP
itab2 = CORRESPONDING #( BASE ( itab2 ) itab1 ). 
```

### Move corresponding using key
```ABAP
itab1 = CORRESPONDING #( itab1 FROM itab2 USING KEY mkey b1 = a1 b2 = a2 ).
```

### Move corresponding for particular entries
```ABAP
    e_header-conditions = VALUE #( FOR condition IN i_head_detail-conditions WHERE ( kschl <> 'MWST' )
  (
    CORRESPONDING #( condition MAPPING type = kschl
                                       rate = kbetr
                                       rate_unit = koein
                                       unit = koei1
                                       description = vtext )
  ) ).
```
