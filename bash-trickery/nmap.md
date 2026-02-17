---
description: various nmap extractors
---

# Nmap

### Scan a list of targets, each entry in the list having their own output .nmap/.gnmap/.xml

This assumes that targets.txt is a list of CIDR defined networks, and there is a created subfolder called scans/

```
   echo "[****] Scanning $line [****]"
   file=$(echo $line | cut -d"/" -f 1)
   sudo nmap -sS --top-ports=1000 -oA scans/$file-targets-top1k-services -vv -A $line 
done < targets.txt
```

### Get a list of hosts with 135, 139 or 445 open

`grep "135\/open\|137\/open\|139\/open\|445\/open" foo.gnmap | cut -d" " -f 2 | sort | uniq`

### Get a list of hosts with 135, 139 or 445 open from a directory structure with lots of gnmaps in

`find . -name *.gnmap -exec cat {} \; | grep "135\/open\|137\/open\|139\/open\|445\/open" | cut -d" " -f 2 | sort | uniq`

### Get a list of uphosts out of a .gnmap

`grep ": Up" foo.gnmap | cut -d" " -f 2 | sort | uniq | awk -vORS=" " '{ print $1 }'`

### Get a list of uphosts with a least one open port out of a .gnmap

`grep "/open/" foo.gnmap | cut -d" " -f 2 | sort | uniq | awk -vORS=" " '{ print $1 }'`

### Convert a .nmap into a list of identified ports

`grep "/tcp" foo.nmap | cut -d"/" -f 1 | sort | uniq | awk -vORS=, '{ print $1 }'`
