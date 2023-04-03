```ABAP
*-----------Declarations----------
TYPES: BEGIN OF st_connection,
             carrier_id      TYPE /dmo/carrier_id,
             connection_id   TYPE /dmo/connection_id,
             airport_from_id TYPE /dmo/airport_from_id,
             airport_to_id   TYPE /dmo/airport_to_id,
             carrier_name    TYPE /dmo/carrier_name,
           END OF st_connection.

    " standard table with non-unique standard key (short form)
    DATA connections_1 TYPE TABLE OF st_connection.
    
    " standard table with non-unique standard key (explicit form)
    DATA connections_2 TYPE STANDARD TABLE OF st_connection
                            WITH NON-UNIQUE DEFAULT KEY.
 
    " sorted table with non-unique explicit key
    DATA connections_3  TYPE SORTED TABLE OF st_connection
                             WITH NON-UNIQUE KEY airport_from_id
                                                 airport_to_id.
    " sorted table with unique explicit key
    DATA connections_5 TYPE SORTED TABLE OF st_connection
                              WITH UNIQUE KEY carrier_id
                                              connection_id.                                             

    " sorted hashed with unique explicit key
    DATA connections_4  TYPE HASHED TABLE OF st_connection
                             WITH UNIQUE KEY carrier_id
                                             connection_id. 
                                             
*-----------Filling Tables----------
* Example 1: APPEND with structured data object (work area)
    " Use VALUE #( ) instead assignment to individual components
    connection = VALUE #( carrier_id       = 'NN'
                          connection_id    = '1234'
                          airport_from_id  = 'ABC'
                          airport_to_id    = 'XYZ'
                          carrier_name     = 'My Airline' ).

    APPEND connection TO connections.

*Example 2: APPEND with VALUE #( ) expression
    APPEND VALUE #( carrier_id       = 'NN'
                    connection_id    = '1234'
                    airport_from_id  = 'ABC'
                    airport_to_id    = 'XYZ'
                    carrier_name     = 'My Airline'
                  )
       TO connections.

* Example 3: Filling an Internal Table with Several Rows
    carriers = VALUE #(  (  carrier_id = 'AA' carrier_name = 'American Airlines' )
                         (  carrier_id = 'JL' carrier_name = 'Japan Airlines'    )
                         (  carrier_id = 'SQ' carrier_name = 'Singapore Airlines')
                      ).

* Example 4: Filling one Internal Table from Another
  connections = CORRESPONDING #( carriers ).

*-----------Accessing Tables----------
      TYPES tt_connections TYPE SORTED TABLE OF   st_connection
                              WITH NON-UNIQUE KEY carrier_id
                                                  connection_id.
   DATA connections TYPE tt_connections.
   DATA connection  LIKE LINE OF connections  
   DATA carriers TYPE STANDARD TABLE OF st_carrier
                       WITH NON-UNIQUE KEY carrier_id.
   DATA carrier LIKE LINE OF carriers.
   
* Table Expression with Key Access  
      " with key fields
    connection = connections[ carrier_id    = 'SQ'
                              connection_id = '0001' ].
    " with non-key fields
    connection = connections[ airport_from_id = 'SFO'
                              airport_to_id   = 'SIN' ].       

* MODIFY TABLE (key access)                             
    carrier = carriers[  carrier_id = 'JL' ].
    carrier-currency_code = 'JPY'.
    MODIFY TABLE carriers FROM carrier.


* MODIFY (index access)
    carrier-carrier_id    = 'LH'.
    carrier-currency_code = 'EUR'.
    MODIFY carriers FROM carrier INDEX 1.

* MODIFY in a LOOP
    LOOP AT carriers INTO carrier
                    WHERE currency_code IS INITIAL.

      carrier-currency_code = 'USD'.
      MODIFY carriers FROM carrier.

    ENDLOOP.
```
