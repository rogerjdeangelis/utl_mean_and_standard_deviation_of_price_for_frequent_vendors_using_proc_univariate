# utl_mean_and_standard_deviation_of_price_for_frequent_vendors_using_proc_univariate
Compute mean and standard deviation for vendors that have more than 3 representatives.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Compute mean and standard deviation for vendors that have more than 3 representatives

    github
    https://tinyurl.com/y6u8jxyb
    https://github.com/rogerjdeangelis/utl_mean_and_standard_deviation_of_price_for_frequent_vendors_using_proc_univariate

    see
    https://tinyurl.com/yavc6qtp
    https://communities.sas.com/t5/SAS-Programming/Is-there-a-way-to-filter-data-during-PROC-UNIVARIATE/m-p/494445

    Compute mean and standard devation for vendors that have more than 3 representatives


    INPUT
    =====

    WORK.HAVE total obs=10

      VENDOR    REP    PRICE

      ACHME      2        8
      ACHME      4        9
      ACHME      1       24
      ACHME      3       25
      ACHME      5       38   Only group with over 3 reps
                              so compute stats fro this group
      4M         1        8
      4M         2        3

      XBC        1       10
      XBC        2       44
      XBC        3       14


    EXAMPLE OUTPUT (only Achme)
    -------------------------
    The UNIVARIATE Procedure
    Variable:  PRICE

    VENDOR = ACHME ==> Only Vendor

                                Moments

    N                           5    Sum Weights                  5
    Mean                     20.8    Sum Observations           104
    Std Deviation      12.5179871    Variance                 156.7
    Skewness           0.30908937    Kurtosis            -1.1699625
    Uncorrected SS           2790    Corrected SS             626.8
    Coeff Variation    60.1826301    Std Error Mean        5.598214

    Frequency Counts for Vendor(ACHME)

                   Percents
     Value Count  Cell   Cum

         8     1  20.0  20.0
         9     1  20.0  40.0
        24     1  20.0  60.0
        25     1  20.0  80.0
        38     1  20.0 100.0


    PROCESS
    =======

    proc univariate freq data=%let rc=%sysfunc(dosubl('
          * filter subroutine;
          proc sql;
            create table subset as
            select * from have group by vendor
            having count(vendor) > 4
         ;quit;

         %let dsn=subset;
        '));
         &dsn;
    var price;
    class vendor;
    id vendor;
    run;quit

    OUTPUT
    ======

    see INPUT

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    data have;
     do vendor="ACHME","4M","XBC";
        do rep=1 to length(vendor);
           price=int(100*uniform(1234));
           output;
        end;
     end;
    run;quit;

    *_
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    ;

    133   proc univariate freq data=%let rc=%sysfunc(dosubl('
    134         * filter subroutine;
    135         proc sql;
    136           create table subset as
    NOTE: The query requires remerging summary statistics back with the original data.
    NOTE: Table WORK.SUBSET created, with 5 rows and 3 columns.

    NOTE: PROCEDURE SQL used (Total process time):
          real time           0.02 seconds
          cpu time            0.01 seconds


    137           select * from have group by vendor
    138           having count(vendor) > 4
    139        ;quit;
    140        %let dsn=subset;
    141       '));
    142        &dsn;
    143   var price;
    144   class vendor;
    145   id vendor;
    146   run;

    NOTE: PROCEDURE UNIVARIATE used (Total process time):
          real time           0.31 seconds
          cpu time            0.12 seconds

    146 !     quit

