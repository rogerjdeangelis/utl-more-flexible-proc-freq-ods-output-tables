# utl-more-flexible-proc-freq-ods-output-tables
Customization is easier if yo ctrate and output ods like table
    More flexible proc freq ods output tables

    Customization is easier if yo ctrate and output ods like table.

    github
    https://tinyurl.com/yb9cao9z
    https://github.com/rogerjdeangelis/utl-more-flexible-proc-freq-ods-output-tables

    StackOverlow
    https://tinyurl.com/y948j768
    https://stackoverflow.com/questions/61484761/sas-newcomer-having-getting-proc-freq-to-show-1-before-0


    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    data have;
     input A62 STATUS2 F;
    cards4;
    0 0 4
    0 1 1
    1 0 3
    1 1 9
    ;;;;
    run;quit;

    WORK.have total obs=4

      A62    STATUS2    F

       0        0       4
       0        1       1
       1        0       3
       1        1       9

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    WORK.WANT total obs=8

      ROWNAM     LEVEL      _1       _0     TOTAL

      COUNT        1       9.00     3.00    12.00
      PERCENT      1      52.94    17.65    70.59
      ROW PCT      1      75.00    25.00      .
      COL PCT      1      90.00    42.86      .
      COUNT        0       1.00     4.00     5.00
      PERCENT      0       5.88    23.53    29.41
      ROW PCT      0      20.00    80.00      .
      COL PCT      0      10.00    57.14      .


    You also have the static output (just highlight the proc freq step and hit LMB;

    Table of A62 by STATUS2

    A62       STATUS2

    Frequency|
    Percent  |
    Row Pct  |
    Col Pct  |       1|       0|  Total
    ---------+--------+--------+
           1 |      9 |      3 |     12
             |  52.94 |  17.65 |  70.59
             |  75.00 |  25.00 |
             |  90.00 |  42.86 |
    ---------+--------+--------+
           0 |      1 |      4 |      5
             |   5.88 |  23.53 |  29.41
             |  20.00 |  80.00 |
             |  10.00 |  57.14 |
    ---------+--------+--------+
    Total          10        7       17
                58.82    41.18   100.00


    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;


    OPTIONS FORMCHAR="|----|+|---+=|-/\<>*";

    proc sort data=have out=havSrt;
       by descending A62 descending status2;
    run;

    %utl_odsfrq(setup);
    Proc Freq data=havSrt order=data;
       Tables A62*Status2;
       weight f;
    run;
    %utl_odsfrq(outdsn=want);




