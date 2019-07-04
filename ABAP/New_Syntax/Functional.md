
### For loop
```ABAP
DATA(result) = VALUE #( FOR row IN input ( row-text ) ). 
* Above syntax does the same as below
" LOOP AT input INTO DATA(row). 
" INSERT row-text INTO TABLE result. 
" ENDLOOP. 
```

### New object creation
```ABAP
DATA(object) = NEW /clean/my_class( ). 
```
