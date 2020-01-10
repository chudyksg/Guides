### Case statement
```ABAP
SELECT vbeln, vbtyp,
 CASE
   WHEN auart = 'ZAMA' THEN @lc_name1
   WHEN auart = 'ZACR' THEN @lc_name2
  ELSE @lc_name3
END AS ernam
FROM vbak
WHERE vbeln = @ld_vbeln
 INTO CORRESPONDING FIELDS of @ls_vbak.
ENDSELECT.
```
### Calculations
```ABAP
DATA: lt_sflight TYPE TABLE OF sflight.

 CONSTANTS: lc_carrid TYPE s_carr_id VALUE 'UA',
            lc_connid TYPE s_conn_id VALUE '941'.

 SELECT carrid, connid, price, seatsocc_b, seatsocc_f,
    ( ( seatsocc_b + seatsocc_f ) ) * price AS paymentsum
    FROM sflight
     WHERE carrid = @lc_carrid
       AND connid = @lc_connid
      INTO CORRESPONDING FIELDS of TABLE @lt_sflight.
```

### Inner Join Column Specification
SELECT scarr~carrname, spfli~*, scarr~url
        FROM scarr INNER JOIN spfli ON scarr~carrid = spfli~carrid
        INTO TABLE @DATA(result).
