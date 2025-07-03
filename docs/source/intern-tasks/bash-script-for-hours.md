# Write a Bash Script to Log Your Hours

*Challange: write a bash script to log your hours.*

---

## Getting Started
Your script should create a pay table that looks similar to this:
```
lgardner|2015-10-06 8:00|2015-10-06 11:30|3.50|MGHPCC/INTERN|Y|N|stuff
```
or 
```
<username>|startdate starttime|enddate endtime|totalhours(rounded to nearest .25)|paycode|billable(y/n)|emergency(y/n)|<notes on what you did>
```

### Tips
- Making default values for your script will make the process of entering your hours signifcantly faster.
- There's a way to have your bash shell get the current date, try using it.
- If you have already finished the Postfix task, consider setting your script to email your hours when prompted.
