# min-max-queries

### Description

`min-max-queries` computes min & max simultaneous queries (or calls) for a specified period with a specified granularity.

The program reads data in files or standard input.

The expected input format is a csv file:
- with 2 columns (a start field followed by a stop field)
- each line must contain a start and stop value with the format "YYYY-MM-DD hh:mm:ss"

A line is used to compute statistics only if a part of the query is contained in the analyzed period.

The program use an array to store query count (1 cell per second).
So, the specified period to analyze is limited to 2678400 seconds (ie 31 days).


### Input 

```bash
 $ head ~/data.csv
 start	end
 2016-06-30 23:59:35	2016-07-01 00:00:41
 2016-06-30 23:58:20	2016-07-01 00:00:20
 2016-06-30 23:58:57	2016-07-01 00:00:51
 2016-06-30 23:59:18	2016-07-01 00:00:02
 2016-06-30 23:58:56	2016-07-01 00:00:26
```  

### Output

```bash
$ ./min-max-queries -m 2016-07 -s $'\t' -g daily -v -i < ~/data.csv 
[============================================================] 100.0% [6163482/6163483] elapsed=1710s left=0s   
start	stop	min	max
2016-07-01 00:00:00	2016-07-01 23:59:59	0	495
2016-07-02 00:00:00	2016-07-02 23:59:59	0	376
2016-07-03 00:00:00	2016-07-03 23:59:59	0	104
2016-07-04 00:00:00	2016-07-04 23:59:59	0	644
2016-07-05 00:00:00	2016-07-05 23:59:59	0	783
2016-07-06 00:00:00	2016-07-06 23:59:59	0	490
2016-07-07 00:00:00	2016-07-07 23:59:59	0	513
2016-07-08 00:00:00	2016-07-08 23:59:59	0	447
2016-07-09 00:00:00	2016-07-09 23:59:59	0	344
2016-07-10 00:00:00	2016-07-10 23:59:59	0	108
2016-07-11 00:00:00	2016-07-11 23:59:59	0	621
2016-07-12 00:00:00	2016-07-12 23:59:59	0	540
2016-07-13 00:00:00	2016-07-13 23:59:59	0	558
2016-07-14 00:00:00	2016-07-14 23:59:59	0	191
2016-07-15 00:00:00	2016-07-15 23:59:59	0	715
2016-07-16 00:00:00	2016-07-16 23:59:59	0	396
2016-07-17 00:00:00	2016-07-17 23:59:59	0	90
2016-07-18 00:00:00	2016-07-18 23:59:59	0	891
2016-07-19 00:00:00	2016-07-19 23:59:59	0	794
2016-07-20 00:00:00	2016-07-20 23:59:59	0	803
2016-07-21 00:00:00	2016-07-21 23:59:59	0	563
2016-07-22 00:00:00	2016-07-22 23:59:59	0	586
2016-07-23 00:00:00	2016-07-23 23:59:59	0	453
2016-07-24 00:00:00	2016-07-24 23:59:59	0	98
2016-07-25 00:00:00	2016-07-25 23:59:59	0	740
2016-07-26 00:00:00	2016-07-26 23:59:59	0	593
2016-07-27 00:00:00	2016-07-27 23:59:59	0	550
2016-07-28 00:00:00	2016-07-28 23:59:59	0	581
2016-07-29 00:00:00	2016-07-29 23:59:59	0	520
2016-07-30 00:00:00	2016-07-30 23:59:59	0	404
2016-07-31 00:00:00	2016-07-31 23:59:59	0	106
min                	2016-07-01 01:15:16	0	-
max                	2016-07-18 10:16:08	-	891
```  


### Options 

#### define the analyzed period

The analyzed period can be defined with the:
- `-m, --month` option
- or `-f, --from` and `-t, --to` options 

#### define the csv separator in input file

To define the field separator in input file, use the `-s, --separator` option.
 
The default separator is `';'`. 

#### ignore the first line of csv files

To ignore the first line of csv files, use the `-i, --ignore` option.

#### set the verbose mode (-v, --verbose)

To display a progress bar, use the `-v, --verbose` option.

```bash
$ ./min-max-queries -m 2016-07 -s $'\t' -g daily -v -i < ~/data.csv 
[==-----------------------------] 6.3% [387278/6163483] elapsed=107s  left=1605s
```  

#### set the report granularity

To define the granularity, use the `-g, --granularity` option.

The available values for this option are :
* daily
* hourly
* Xh where X is a number (every X hours)
* Xm where X is a number (every X minutes)

