# utl-sending-a-formula-to-excel-to-reference-a-cell-in-another-sheet
Sending a formula to excel to reference a cell in another sheet
    Sending a formula to excel to reference a cell in another sheet

    github
    https://tinyurl.com/y583zm4t
    https://github.com/rogerjdeangelis/utl-sending-a-formula-to-excel-to-reference-a-cell-in-another-sheet

    Other excel repos
    https://tinyurl.com/ybnm6azh
    https://github.com/rogerjdeangelis?utf8=%E2%9C%93&tab=repositories&q=excel+in%3Aname&type=&language=

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    * create a workbook with two worksheets;

    %let formula=sex!B2;

    %utlfkil(d:/xls/class.xlsx);

    libname xel "d:/xls/class.xlsx";
    data xel.names(keep=name sex) xel.sex(keep=name sex);
      set sashelp.class(obs=1);
      output xel.sex;
      sex="";
      output xel.names;
    run;quit;
    libname xel clear;


    Workbook d:/xls/class.xlsx  with two sheets, names and sex

    d:/xls/class.xlsx

      +-------------------------+
      |     A      |    B       |
      +-------------------------+
    1 |  NAME      |   SEX      |
      +------------+------------+
    2 | ALFRED     |            |   * value for sex is in worksheet sex
      +------------+------------+

    [NAMES]


      +-------------------------+
      |     A      |    B       |
      +-------------------------+
    1 |  NAME      |   SEX      |
      +------------+------------+
    2 | ALFRED     |    M       |   * has the value I want worksheet names to reference
      +------------+------------+

    [SEX]  * second worksheet


    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    When I open worksheet names 'M'

    d:/xls/class.xlsx

    +----------------------+
    |   B2    Fx   =sex!B2 |
    +----------------------+
      +-------------------------+
      |     A      |    B       |
      +-------------------------+
    1 |  NAME      |   SEX      |
      +------------+------------+  Get sex from worksheet 'sex'
    2 | ALFRED     |    M       |  =sex!B2 is in this cell
      +------------+------------+

    [NAMES]

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %let formula=sex!B2;

    %utlfkil(d:/xls/class.xlsx);

    libname xel "d:/xls/class.xlsx";
    data xel.names(keep=name sex) xel.sex(keep=name sex);
      set sashelp.class(obs=1);
      output xel.sex;
      sex="";
      output xel.names;
    run;quit;
    libname xel clear;


    %let formula=sex!B2;

    %utl_submit_r64("
    library(XLConnect);
    wb <- loadWorkbook('d:/xls/class.xlsx', create = FALSE);
    setCellFormula(wb, 'names', 2, 2, '&formula');
    saveWorkbook(wb);
    ");

