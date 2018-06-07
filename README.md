# utl_add_a_column_to_sql_when_it_does_not_exist
In SQL add a numeric column only if it does not exist, if it exists do not corrupt the value.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    In SQL add a numeric column only if it does not exist, if it exists do not corrupt the value

    see
    https://tinyurl.com/yaspuqbh
    https://communities.sas.com/t5/Base-SAS-Programming/PROC-SQL-Case-colulmn-exists-or-does-not-exists/m-p/468310

    HAVE  ( Two test cases)

    Age missing

     WORK.NOAGE total obs=3 (Column age not present)

         NAME      SEX    HEIGHT    WEIGHT

        Alfred      M      69.0      112.5
        Alice       F      56.5       84.0
        Barbara     F      65.3       98.0

     WORK.hasAge total obs=3

        NAME      SEX    AGE    HEIGHT    WEIGHT

       Alfred      M      14     69.0      112.5
       Alice       F      13     56.5       84.0
       Barbara     F      13     65.3       98.0


    EXAMPLE OUTPUT

      ADD AGE  because it does not exist

       WORK.WANT total obs=3

          NAME      AGE    SEX    HEIGHT    WEIGHT

         Alfred      23     M      69.0      112.5
         Alice       23     F      56.5       84.0
         Barbara     23     F      65.3       98.0\


      AGE EXITS Do not corrupt AGE

       WORK.WANT total obs=3

         NAME      AGE    SEX    HEIGHT    WEIGHT

        Alfred      14     M      69.0      112.5
        Alice       13     F      56.5       84.0
        Barbara     13     F      65.3       98.0


    PROCESS  (works for both input datasets)
    =======

      proc sql;
        create
           table want as
        select
            name
           ,age
           ,sex
           ,height
           ,weight
        from
           %let rc=%sysfunc(dosubl('data havVue/view=havVue;retain age 23;;set hasAge;run;quit;'));
           havVue
      ;quit;


    OUTPUT
    ======

      ADD AGE  because it does not exist

       WORK.WANT total obs=3

          NAME      AGE    SEX    HEIGHT    WEIGHT

         Alfred      23     M      69.0      112.5
         Alice       23     F      56.5       84.0
         Barbara     23     F      65.3       98.0\


      AGE EXITS Do not corrupt AGE

       WORK.WANT total obs=3

         NAME      AGE    SEX    HEIGHT    WEIGHT

        Alfred      14     M      69.0      112.5
        Alice       13     F      56.5       84.0
        Barbara     13     F      65.3       98.0

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;
     * age missing;
     data noAge;
       set sashelp.class(obs=3 drop=age);
     run;quit;

     * age present;
     data hasAge;
       set sashelp.class(obs=3);
     run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;


    see process

