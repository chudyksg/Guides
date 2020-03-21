
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
  
  ### LOOP AT with GROUP BY
  More info: http://zevolving.com/2015/10/abap-740-loop-at-with-group-by/
* GROUP BY Syntax
```ABAP
  LOOP AT t_customres INTO DATA(ls_cust1)
     GROUP BY  ( route = ls_cust1-route
                 SIZE  = GROUP SIZE
                 INDEX = GROUP INDEX )
      ASCENDING
      REFERENCE INTO DATA(route_group).
  ```
  * Get Unique values using the GROUP BY
```ABAP
TYPES: BEGIN OF ty_customer,
    customer TYPE char10,
    NAME     TYPE char30,
    city     TYPE char30,
    route    TYPE char10,
  END   OF ty_customer.
TYPES: tt_customers TYPE SORTED TABLE OF ty_customer
          WITH UNIQUE KEY customer.
 
TYPES: tt_citys TYPE STANDARD TABLE OF char30 WITH EMPTY KEY.
 
DATA(t_customres) =
VALUE tt_customers(
  ( customer = 'C0001' NAME = 'Test Customer 1' city = 'NY' route = 'R0001' )
  ( customer = 'C0002' NAME = 'Customer 2'      city = 'LA' route = 'R0003' )
  ( customer = 'C0003' NAME = 'Good Customer 3' city = 'DFW' route = 'R0001' )
  ( customer = 'C0004' NAME = 'Best Customer 4' city = 'CH' route = 'R0003' )
  ( customer = 'C0005' NAME = 'So So Customer 5' city = 'NY' route = 'R0001' )
).
 
* Simply get the unique Routes, use WITHOUT MEMBERS
LOOP AT t_customres INTO DATA(ls_cust_2)
     GROUP BY  ( route = ls_cust_2-route )
      ASCENDING
      WITHOUT MEMBERS
      REFERENCE INTO DATA(route_group_2).
      
       WRITE: / route_group_2->route.
ENDLOOP. 
```

* Usage of MEMBERS, SIZE and INDEX
```ABAP
* Creates a group of Route
*   with members as all fields which matches the group
LOOP AT t_customres INTO DATA(ls_cust1)
     GROUP BY  ( route = ls_cust1-route
                 SIZE  = GROUP SIZE
                 INDEX = GROUP INDEX )
      ASCENDING
      REFERENCE INTO DATA(route_group).
 
  WRITE: / 'Group', route_group->index.
  WRITE: / route_group->route.
 
  DATA(members) = VALUE tt_customers( ).
  LOOP AT GROUP route_group ASSIGNING FIELD-SYMBOL(<route>).
    members = VALUE #( BASE members ( <route> ) ).
  ENDLOOP.
 
  LOOP AT members INTO DATA(ls_member).
    WRITE: /(5)", ls_member-customer, ls_member-name, ls_member-city.
  ENDLOOP.
  WRITE: /(5)", 'Group size ', route_group->size.
  SKIP 2.
ENDLOOP.
```
* Group By without explicit Result variable
```ABAP
 
* Creates a group of Route and City
*  but without using the Group result
LOOP AT t_customres INTO DATA(ls_cust)
     GROUP BY  ( route = ls_cust-route
                 city  = ls_cust-city )
      ASCENDING.
 
  WRITE: / ls_cust.
 
  DATA(members) = VALUE tt_customers( ).
  LOOP AT GROUP ls_cust ASSIGNING FIELD-SYMBOL(<route>).
    members = VALUE #( BASE members ( <route> ) ).
  ENDLOOP.
 
  LOOP AT members INTO DATA(ls_member).
    WRITE: /(5)", ls_member-customer, ls_member-name.
  ENDLOOP.
  SKIP 2.
ENDLOOP.
```

* Loop with control break
```ABAP
 DATA(out) = cl_demo_output=>new( ).
    DATA members LIKE flights.
    LOOP AT flights INTO DATA(wa)
         GROUP BY ( tz_from = get_time_zone( wa-airpfrom )
                    tz_to   = get_time_zone( wa-airpto )
                    size = GROUP SIZE index = GROUP INDEX )
         ASSIGNING FIELD-SYMBOL(<group>).
      out->write( name = `Group key`
                  data = <group> ).
      CLEAR members.
      LOOP AT GROUP <group> ASSIGNING FIELD-SYMBOL(<member>).
        members = VALUE #( BASE members ( <member> ) ).
      ENDLOOP.
      out->write( members )->line( ).
    ENDLOOP.
    out->display( ).
```

* Another loop group by
```ABAP
    LOOP AT me->go_data->gt_processing_log INTO DATA(ls_processing_log)
                                           WHERE icon = me->go_data->gc_red_light
                                           GROUP BY ( requisition = ls_processing_log-requisition  )
                                           ASSIGNING FIELD-SYMBOL(<group>).

      LOOP AT GROUP <group> INTO DATA(ls_error_log).
      ENDLOOP.
    ENDLOOP.
```

### Reduce
```ABAP
DATA(lv_lines) = REDUCE i( INIT x = 0 FOR wa IN gt_itab WHERE( F1 = 'XYZ' ) NEXT x = x + 1 ).

*Below is the same as code above
LOOP AT gt_itab INTO ls_itab where F1 = 'XYZ'.
  lv_lines = lv_lines + 1.
ENDLOOP.
```  
  
