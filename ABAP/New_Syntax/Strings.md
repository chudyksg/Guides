### Chaining Operator
```ABAP
DATA(lv_result) = v_var1 && v_var2 && v_var3. 
```
### String templates
```ABAP
character_string = |This is a literal text.|. 
character_string = |{ a_numeric_variable }|. 
character_string = |This resulted in return code { sy-subrc }|. 
```
### Embedded Expressions
```ABAP
* Delivery number with conversion
DATA(ld_message) = |{ ld_delivery_number ALPHA = OUT }|. 
```
