# maxqueries

## Description

`maxqueries` is a tool to compute minimal, maximal of simultaneous queries for a specified month.

It reads data in files or standard streams.

The entry set must be datetime fields with the mySQL format (ex: 2016-09-14 15:26:52)

## Input format

The input format is a `csv` file. It must contains a beginning datetime followed by a ending datetime.

```bash
  $ grep 2016-07-01 ~/data.csv | head
  2016-06-30 23:59:35	2016-07-01 00:00:41
  2016-06-30 23:58:20	2016-07-01 00:00:20
  2016-06-30 23:58:57	2016-07-01 00:00:51
```  

#### Option --separator
The field separator can be defined with the `-s` (`--separator`) option. The default field separator is `;`.

#### Option --ignore
If the first line in input files or streams must be ignored, the `-i` (`--ignore`) option must be set.



## Output format


#### Option --month

The `-m` (`--month`) option defines the analyzed month.

An entry could start before the begin of the analyzed month and could end after the end of the month.
    
A such entry is used to compute the analyzed month.    

#### Option --period

The `-p` (`--period`) option defines the granularity period for the report.

The available values for this option are :
* daily
* hourly
* Xh where X is a number (every X hours)
* Xm where X is a number (every X minutes)

## Examples of reports 
 
#### one line per day
 
```
  $ ./maxqueries -m 2016-07 -s $'\t' -p daily -i ~/data.csv
  >period                          min     max
  [01@00:00:00->01@23:59:59]	0	502	
  [02@00:00:00->02@23:59:59]	0	380	
  [03@00:00:00->03@23:59:59]	0	104	
  [04@00:00:00->04@23:59:59]	0	651	
  [05@00:00:00->05@23:59:59]	0	797	
  [06@00:00:00->06@23:59:59]	0	496	
  [07@00:00:00->07@23:59:59]	0	518	
  [08@00:00:00->08@23:59:59]	0	453	
  [09@00:00:00->09@23:59:59]	0	347	
  [10@00:00:00->10@23:59:59]	0	108	
  [11@00:00:00->11@23:59:59]	0	631	
  [12@00:00:00->12@23:59:59]	0	550	
  [13@00:00:00->13@23:59:59]	0	564	
  [14@00:00:00->14@23:59:59]	0	192	
  [15@00:00:00->15@23:59:59]	0	719	
  [16@00:00:00->16@23:59:59]	0	402	
  [17@00:00:00->17@23:59:59]	0	91	
  [18@00:00:00->18@23:59:59]	0	903	
  [19@00:00:00->19@23:59:59]	0	803	
  [20@00:00:00->20@23:59:59]	0	814	
  [21@00:00:00->21@23:59:59]	0	571	
  [22@00:00:00->22@23:59:59]	0	593	
  [23@00:00:00->23@23:59:59]	0	458	
  [24@00:00:00->24@23:59:59]	0	99	
  [25@00:00:00->25@23:59:59]	0	750	
  [26@00:00:00->26@23:59:59]	0	597	
  [27@00:00:00->27@23:59:59]	0	557	
  [28@00:00:00->28@23:59:59]	0	585	
  [29@00:00:00->29@23:59:59]	0	525	
  [30@00:00:00->30@23:59:59]	0	407	
  [31@00:00:00->31@23:59:59]	0	107	
  min     0       01@01:15:17
  max     502     01@10:47:21

```
 
#### one line per hour
  
In the followed example, only the result for the first day is displayed (because of `grep -F '[01@'`)  
  
```  
  $ ./maxqueries -m 2016-07 -s $'\t' -p hourly -i <( grep 2016-07-01 ~/data.csv) | grep -F '01@'
  [01@00:00:00->01@00:59:59]	2	21	
  [01@01:00:00->01@01:59:59]	0	13	
  [01@02:00:00->01@02:59:59]	0	6	
  [01@03:00:00->01@03:59:59]	0	7	
  [01@04:00:00->01@04:59:59]	0	5	
  [01@05:00:00->01@05:59:59]	0	9	
  [01@06:00:00->01@06:59:59]	1	31	
  [01@07:00:00->01@07:59:59]	11	158	
  [01@08:00:00->01@08:59:59]	146	323	
  [01@09:00:00->01@09:59:59]	292	433	
  [01@10:00:00->01@10:59:59]	371	502	
  [01@11:00:00->01@11:59:59]	321	483	
  [01@12:00:00->01@12:59:59]	249	358	
  [01@13:00:00->01@13:59:59]	252	387	
  [01@14:00:00->01@14:59:59]	306	441	
  [01@15:00:00->01@15:59:59]	336	467	
  [01@16:00:00->01@16:59:59]	348	472	
  [01@17:00:00->01@17:59:59]	322	462	
  [01@18:00:00->01@18:59:59]	232	430	
  [01@19:00:00->01@19:59:59]	129	299	
  [01@20:00:00->01@20:59:59]	63	168	
  [01@21:00:00->01@21:59:59]	28	85	
  [01@22:00:00->01@22:59:59]	9	53	
  [01@23:00:00->01@23:59:59]	1	29
  min     0       01@01:15:17
  max     502     01@10:47:21
	
```
