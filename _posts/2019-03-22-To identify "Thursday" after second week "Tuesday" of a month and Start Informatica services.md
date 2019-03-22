---
layout: post
title: PYTHON - To identify "Thursday" after second week "Tuesday" of a month
---

{{ page.title }}
================


import calendar

from datetime import datetime

import subprocess

currentMonth = datetime.now().month

currentYear = datetime.now().year

currentDay = datetime.now().day


c = calendar.monthcalendar(currentYear,currentMonth)

first_week = c[0]

second_week = c[1]

third_week = c[2]

if first_week[calendar.TUESDAY]:

 patch_date = second_week[calendar.TUESDAY]
 
else:

 patch_date = third_week[calendar.TUESDAY]

patch_date=patch_date+2

if currentDay==patch_date:

 subprocess.Popen(['sh','/home/infaprd/start_infa.sh'])
 
else:

 print("Dates not matching")
