### Chaining Operator
```ABAP
DATA(lv_result) = v_var1 && v_var2 && v_var3. 
```
### Concatenation
```ABAP
DATA(lv_out) = |Hello| & | | & |world|.
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
### Upper, lower case
```ABAP
DATA(uppercase) = to_upper( lowercase ). 
DATA(lowercase) = to_lower( uppercase ). 
```
### Width/Alignment/Padding
```ABAP
WRITE / |{ 'Left'     WIDTH = 20 ALIGN = LEFT   PAD = '0' }|.
WRITE / |{ 'Centre'   WIDTH = 20 ALIGN = CENTER PAD = '0' }|.
WRITE / |{ 'Right'    WIDTH = 20 ALIGN = RIGHT  PAD = '0' }|.
```
### Case
```ABAP
WRITE / |{ 'Text' CASE = (cl_abap_format=>c_raw) }|.
WRITE / |{ 'Text' CASE = (cl_abap_format=>c_upper) }|.
WRITE / |{ 'Text' CASE = (cl_abap_format=>c_lower) }|.
```

### ALPHA conversion
```ABAP
DATA(lv_vbeln) = '0000012345'.
WRITE / |{ lv_vbeln  ALPHA = OUT }|.     “or use ALPHA = IN to go in other direction
```

### Date conversion
```ABAP
WRITE / |{ pa_date DATE = ISO }|.           “Date Format YYYY-MM-DD
WRITE / |{ pa_date DATE = User }|.          “As per user settings
WRITE / |{ pa_date DATE = Environment }|.   “Formatting setting of language environment
```
