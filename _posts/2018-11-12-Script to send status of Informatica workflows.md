---
layout: post

title: UNIX - Script to send status of Informatica workflows
---



{{ page.title }}

================


#!/bin/bash
source $HOME/.bash_profile

output=/home/cron/output.lst

wfVAR="wf_Workflow1 wf_Workflow2 wf_Workflow3"

sqlplus -s scott/tiger@DBNAME <<EOF > $output   # Capture output from SQL
        
prompt 1) Transactions between 8am Yesterday and 8am Today

set linesize 55 pages 500

spool output_temp.lst;

set head off;

select STATUS,count(*) from TABLENAME where CREATED BETWEEN sysdate-1 AND
sysdate
group by status;

set head on;

spool off;

EOF

INFA_OK=`ps -ef | grep -c "$INFA_HOME"`

B2B_OK=`ps -ef | grep -c "B2B"`

MQ_OK=`ps -ef | grep -c "activemq"`

if [ $INFA_OK -gt 9 ] && [ $B2B_OK -gt 9 ]

then

        echo "2) All Informatica Services Running" >> $output
        
else

        echo "2) Informatica Services Down" >> $output
        
fi

echo >> $output

if [ $MQ_OK -gt 1 ]

then

        echo "3) ActiveMQ Services Running" >> $output
        
else

        echo "3) ActiveMQ Services Down" >> $output
        
fi

echo >> $output

echo "4) Informatica workflows from last night and this morning:-" >> $output

echo >> $output

echo "Workflow Name                                              Status           End Time" >> $output

echo "--------------------                                              ---------          -----------" >> $output

echo >> $output

for name in ${wfVAR}; do

  pmcmd getworkflowdetails -sv INFA_REPO -d INFA_DOMAIN -u Admin -p Password -usd Native -f "Folder Name" ${name}
  
done |

grep -e "Workflow:" -e "Workflow run status:" -e "End time:" | cut -d'[' -f2 | cut -d']' -f1 |

awk '{printf "%s%s",$0,NR%3?" :-\t":"\n""\n" ; }' >> $output

mail -s "Morning Checks -Infa - `date '+%d-%m-%y'`" email@gmaill.com <$output
