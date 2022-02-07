### Submit RHINTE30
```
FORM update_pa_om_integration  USING i_pernr TYPE pernr_d.
  DATA stamp TYPE sy-uzeit.
  DATA lv_groupname TYPE apqi-groupid.
  DATA ls_apqi TYPE apqi.

*Submit RHINTE30 which creates a batch input session
  SUBMIT rhinte30 WITH pnptimr6 = 'X'
                  WITH pnppernr-low = i_pernr
                  WITH test = ''
                  WITH show = 'X'
                  WITH open = '' EXPORTING LIST TO MEMORY AND RETURN.

*Import the time stamp in order recreate the batch input session name created
*by RHINTE 30. It is exported in RHINTE30. line 431
  IMPORT stamp FROM MEMORY ID 'INTEBATCH'.
  IF sy-subrc = 0 AND NOT stamp IS INITIAL.

    lv_groupname = sy-uname.
    lv_groupname+6(6) = stamp.

*Check if thes batch input sessione exists
    SELECT SINGLE *
      FROM apqi
      INTO ls_apqi
      WHERE datatyp = 'BDC'
      AND   groupid = lv_groupname
      AND   progid = 'RHINTE30'.

    IF sy-subrc = 0.
      SUBMIT rsbdcsub WITH mappe = lv_groupname
                      WITH z_verarb = 'X'
                      WITH fehler = ''
                      EXPORTING LIST TO MEMORY AND RETURN.

    ENDIF.
  ENDIF.
ENDFORM.                    " UPDATE_PA_OM_INTEGRATION

```
