### SWITCH Statement
More info: http://zevolving.com/2015/10/abap-740-switch-conditional-operator/
```ABAP
DATA(lv_status) = SWITCH #( lv_flag
                              WHEN 'X' THEN 'Passed'
                              ELSE 'failed'
                          ).
```

### XSD Boolean
```ABAP
DATA(has_entries) = xsdbool( line IS NOT INITIAL ).
IF has_entries = abap_true.
ENDIF.
```
