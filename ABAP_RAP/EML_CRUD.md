### Read
```ABAP
    READ ENTITY Z_C_USERINFO
        ALL FIELDS
            "FIELDS ( Email first_name last_name )
                WITH VALUE #(  (

                        Email = 'Alex@demo.com'

                    )
                    (

                        Email = 'DEMO1@DEMO1.com'

                    )

                 )
                RESULT DATA(lt_read_user).
                "REPORTED reported
                "FAILED failed.

```

### Update
```ABAP
MODIFY ENTITY Z_C_USERINFO
           UPDATE FIELDS ( first_name last_name ) WITH
           "UPDATE FROM
                 VALUE #(
                        (
                          Email = 'Alex@demo.com'
                          first_name = 'New'
                          last_name = 'Name'
                          "%control-first_name = if_abap_behv=>mk-on
                          "%control-last_name = if_abap_behv=>mk-on


                        )
                     ).
                      "REPORTED reported
                       "FAILED failed.

COMMIT ENTITIES.
```                    
### Create
```ABAP
         MODIFY ENTITY Z_C_USERINFO
             CREATE FIELDS  ( Email first_name last_name is_admin last_changed_at )
                 WITH VALUE
                     #( (
                      Email = 'new@demo.com'
                      first_name = 'New'
                      last_name = 'Entry'
                      is_admin  = 'No'
                      last_changed_at = lt_ts

                ) ).
 COMMIT ENTITIES.               
 ```               
### Delete
```ABAP
   MODIFY ENTITY Z_C_USERINFO
            DELETE FROM VALUE #( (
                    Email = 'new@demo.com'

                ) ).
 COMMIT ENTITIES.               
 ```                 
