
### For iteration
Detailed info: http://zevolving.com/2015/05/abap-740-for-iteration-expression/
* Append value of 1 field into another table
```ABAP
DATA(t_result) = VALUE #( FOR row IN t_input ( row-text ) ). 
* Above syntax does the same as below
" LOOP AT t_input INTO DATA(row). 
" INSERT row-text INTO TABLE t_result. 
" ENDLOOP. 
```
* FOR with WHERE condition
```ABAP
DATA(t_city_in_03) = VALUE tt_citys( FOR ls_cust IN t_customres WHERE ( route = 'R0001' ) ( ls_cust-city ) ).
```
* Nested FOR - 2 levels
```ABAP
DATA(t_route_names) =
  VALUE tt_names(
    FOR ls_cust_1 IN t_customres
    FOR ls_route  IN t_routes WHERE ( route = ls_cust_1-route )
    ( ls_route-NAME )
  ).
```
* Nested LOOP with multiple tables
```ABAP
DATA(t_routes_max) =
  VALUE tt_routes_max(
    FOR ls_cust_2   IN t_customres
    FOR ls_route_2  IN t_routes WHERE ( route = ls_cust_2-route )
    FOR ls_rc_2     IN t_rc     WHERE ( route = ls_route_2-route
                                   AND  c_type = 'MAX' )
    ( route = ls_route_2-route
      NAME  = ls_route_2-NAME
      c_value = ls_rc_2-c_value )
  ).
  ```
  
  * LET with specific (and default) value with FOR
  ```ABAP
  DATA(t_routes_cust) =
  VALUE tt_routes_cust(
    FOR ls_cust_l   IN t_customres
      INDEX INTO cust_index
      "where ( customer = 'C0001' )
      LET  lv_name   =  t_routes[ route = t_customres[ cust_index ]-route ]-NAME
           lv_route  =  t_routes[ 1 ]-route
           IN NAME = lv_name
              route = lv_route
    ( customer = ls_cust_l-customer )
  ).
  ```
  * FOR with LET to populate the RANGE
  ```ABAP
TYPES: tt_route_range TYPE RANGE OF char10.
 
DATA(t_route_range) =
  VALUE tt_route_range(
    "( sign = 'I' option = 'BT' low = '001' high = '002' )
    FOR ls_cust_r IN t_customres
      LET s = 'I'
          o = 'EQ'
        IN SIGN     = s
           OPTION   = O
    ( LOW = ls_cust_r-route )
  ).
  ```

### New object creation
```ABAP
DATA(object) = NEW /clean/my_class( ). 
```
