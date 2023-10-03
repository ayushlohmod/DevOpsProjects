
# 90 Days Of DevOps

## Log

### Day 000: Sep 24, 2023 (Script)

**Today's Progress**:

Today created a Bash script to monitor disk usage on a system and raise a "CRITICAL" alert if any of the disk partitions have usage greater than or equal to the specified threshold, which is set to 90% (alert=90).

```
#!/bin/bash
alert=90
df -H | awk '{print $5 " " $1}' | while read output;
do
#echo "Disk Detail: $output"
 usage=$(echo $output | awk '{print $1}' | cut -d'%' -f1)
 file_sys=$(echo $output | awk '{print $2}i')
 #echo $usage
if [ $usage -ge $alert ]
 then
        echo "CRITICAL for $file_sys"
fi
done
    
```

### Day 000: Oct 1, 2023 (DockerFile)

**Today's Progress**:
Today created a docker files 
