
# Hitachi 7200

## EXT4  
  
### Preparation

```bash
mkfs.ext4 /dev/sde1 -m 0 -T largefile  
```
  
#### Individual disk

```
/dev/sde1 3904735508 90140 3904628984 1% /mnt/ext4  
```
  
#### QNAP HW RAID 0 & JBOD  
  
```
/dev/sdb1 15621840372 3164828 15618659160 1% /mnt/ext4  
```
  
### Testing
  
#### Individual disk  

```bash
dd if=/dev/zero of=ext4/smallblock.test bs=1M count=1024 oflag=dsync status=progress  
1071644672 bytes (1.1 GB, 1022 MiB) copied, 58 s, 18.5 MB/s  
1024+0 records in  
1024+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 58.1221 s, 18.5 MB/s  
```

```bash
dd if=/dev/zero of=ext4/bigblock.test bs=1G count=1 oflag=dsync status=progress  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 8 s, 133 MB/s  
1+0 records in  
1+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 8.0838 s, 133 MB/s  
```

```bash
dd if=/dev/zero of=ext4/latency.test bs=512 count=1000 oflag=dsync  
1000+0 records in  
1000+0 records out  
512000 bytes (512 kB, 500 KiB) copied, 49.9166 s, 10.3 kB/s  
```

```bash
flush
echo 3 | sudo tee /proc/sys/vm/drop_caches
dd if=ext4/read.test of=/dev/null  
2097152+0 records in  
2097152+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 2.42411 s, 443 MB/s  
```

```bash
hdparm -t -T /dev/sdd1  
  
/dev/sdd1:  
Timing cached reads: 23560 MB in 1.99 seconds = 11848.18 MB/sec  
Timing buffered disk reads: 442 MB in 3.00 seconds = 147.30 MB/sec  
```

#### QNAP HW RAID 0  

```bash
dd if=/dev/zero of=ext4/smallblock.test bs=1M count=1024 oflag=dsync status=progress  
1066401792 bytes (1.1 GB, 1017 MiB) copied, 56 s, 19.0 MB/s  
1024+0 records in  
1024+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 56.3928 s, 19.0 MB/s  
```

```bash
dd if=/dev/zero of=ext4/bigblock.test bs=1G count=1 oflag=dsync status=progress  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 5 s, 197 MB/s  
1+0 records in  
1+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 5.44522 s, 197 MB/s  
```

```bash
dd if=/dev/zero of=ext4/latency.test bs=512 count=1000 oflag=dsync  
1000+0 records in  
1000+0 records out  
512000 bytes (512 kB, 500 KiB) copied, 71.279 s, 7.2 kB/s  
```

```bash
flush
echo 3 | sudo tee /proc/sys/vm/drop_caches
dd if=ext4/read.test of=/dev/null  
2097152+0 records in  
2097152+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 5.63322 s, 191 MB/s  
```

```bash
hdparm -t -T /dev/sdb1  
  
/dev/sdb1:  
Timing cached reads: 25056 MB in 1.99 seconds = 12603.82 MB/sec  
Timing buffered disk reads: 686 MB in 3.01 seconds = 228.13 MB/sec  
```

#### QNAP HW JBOD  

```bash
dd if=/dev/zero of=ext4/smallblock.test bs=1M count=1024 oflag=dsync status=progress  
1064304640 bytes (1.1 GB, 1015 MiB) copied, 26 s, 40.9 MB/s  
1024+0 records in  
1024+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 26.2311 s, 40.9 MB/s  
```

```bash
dd if=/dev/zero of=ext4/bigblock.test bs=1G count=1 oflag=dsync status=progress  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 8 s, 138 MB/s  
1+0 records in  
1+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 7.79827 s, 138 MB/s  
```

```bash
dd if=/dev/zero of=ext4/latency.test bs=512 count=1000 oflag=dsync  
1000+0 records in  
1000+0 records out  
512000 bytes (512 kB, 500 KiB) copied, 17.4423 s, 29.4 kB/s  
```

```bash
flush
echo 3 | sudo tee /proc/sys/vm/drop_caches
dd if=ext4/read.test of=/dev/null  
2097152+0 records in  
2097152+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 2.42558 s, 443 MB/s  
```

```bash
hdparm -t -T /dev/sdb1  
  
/dev/sdb1:  
Timing cached reads: 24166 MB in 1.99 seconds = 12153.32 MB/sec  
Timing buffered disk reads: 466 MB in 3.00 seconds = 155.32 MB/sec  
```

## xfs  
  
### Preparation  

```bash
mkfs.xfs /dev/sde1  
```

https://wiki.archlinux.org/title/XFS#Stripe_size_and_width  
  
#### Individual disk  

```
/dev/sdd1 3905109820 30405692 3874704128 1% /mnt/xfs 
``` 
  
#### QNAP HW RAID 0 & JBOD  

```
/dev/sdb1 15625757676 108978584 15516779092 1% /mnt/xfs 
```
  
### Testing  
  
#### Individual disk  

```bash
dd if=/dev/zero of=xfs/smallblock.test bs=1M count=1024 oflag=dsync status=progress  
1064304640 bytes (1.1 GB, 1015 MiB) copied, 47 s, 22.6 MB/s  
1024+0 records in  
1024+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 47.4429 s, 22.6 MB/s  
```

```bash
dd if=/dev/zero of=xfs/bigblock.test bs=1G count=1 oflag=dsync status=progress  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 7 s, 151 MB/s  
1+0 records in  
1+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 7.10065 s, 151 MB/s  
```

```bash
dd if=/dev/zero of=xfs/latency.test bs=512 count=1000 oflag=dsync  
1000+0 records in  
1000+0 records out  
512000 bytes (512 kB, 500 KiB) copied, 38.0415 s, 13.5 kB/s  
```

```bash
flush
echo 3 | sudo tee /proc/sys/vm/drop_caches
dd if=xfs/read.test of=/dev/null  
2097152+0 records in  
2097152+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 2.45509 s, 437 MB/s  
```

```bash
hdparm -t -T /dev/sdd1  
  
/dev/sdd1:  
Timing cached reads: 23216 MB in 1.99 seconds = 11672.64 MB/sec  
Timing buffered disk reads: 490 MB in 3.01 seconds = 162.70 MB/sec  
```

#### QNAP HW RAID 0  

```bash
dd if=/dev/zero of=xfs/smallblock.test bs=1M count=1024 oflag=dsync status=progress  
1059061760 bytes (1.1 GB, 1010 MiB) copied, 62 s, 17.1 MB/s  
1024+0 records in  
1024+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 62.8997 s, 17.1 MB/s  
```

```bash
dd if=/dev/zero of=xfs/bigblock.test bs=1G count=1 oflag=dsync status=progress  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 5 s, 218 MB/s  
1+0 records in  
1+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 4.91839 s, 218 MB/s  
```

```bash
dd if=/dev/zero of=xfs/latency.test bs=512 count=1000 oflag=dsync  
1000+0 records in  
1000+0 records out  
512000 bytes (512 kB, 500 KiB) copied, 61.187 s, 8.4 kB/s  
```

```bash
flush
echo 3 | sudo tee /proc/sys/vm/drop_caches
dd if=xfs/read.test of=/dev/null  
2097152+0 records in  
2097152+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 2.51808 s, 426 MB/s  
```

```bash
hdparm -t -T /dev/sdb1  
  
/dev/sdb1:  
Timing cached reads: 25220 MB in 1.99 seconds = 12686.68 MB/sec  
Timing buffered disk reads: 752 MB in 3.00 seconds = 250.43 MB/sec  
```

#### QNAP HW JBOD  

```bash
dd if=/dev/zero of=xfs/smallblock.test bs=1M count=1024 oflag=dsync status=progress  
1030750208 bytes (1.0 GB, 983 MiB) copied, 19 s, 54.2 MB/s  
1024+0 records in  
1024+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 19.7541 s, 54.4 MB/s  
```

```bash
dd if=/dev/zero of=xfs/bigblock.test bs=1G count=1 oflag=dsync status=progress  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 7 s, 151 MB/s  
1+0 records in  
1+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 7.13312 s, 151 MB/s  
```

```bash
dd if=/dev/zero of=xfs/latency.test bs=512 count=1000 oflag=dsync  
1000+0 records in  
1000+0 records out  
512000 bytes (512 kB, 500 KiB) copied, 11.5232 s, 44.4 kB/s  
```

```bash
flush
echo 3 | sudo tee /proc/sys/vm/drop_caches
dd if=xfs/read.test of=/dev/null  
2097152+0 records in  
2097152+0 records out  
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 2.45856 s, 437 MB/s  
```

```bash
hdparm -t -T /dev/sdb1  
  
/dev/sdb1:  
Timing cached reads: 25472 MB in 1.99 seconds = 12814.07 MB/sec  
Timing buffered disk reads: 474 MB in 3.01 seconds = 157.68 MB/sec
```

## Results

### Write throughput small block

Config | FileSystem | Speed (MB/s)
---|---|---
Individual|ext4|18.5
Individual|xfs|22.6
QNAP HW RAID 0|ext4|19.0
QNAP HW RAID 0|xfs|17.1
QNAP HW JBOD|ext4|40.9
QNAP HW JBOD|xfs|54.4


### Write throughput big block

Config | FileSystem | Speed (MB/s)
---|---|---
Individual|ext4|133
Individual|xfs|151
QNAP HW RAID 0|ext4|197
QNAP HW RAID 0|xfs|218
QNAP HW JBOD|ext4|138
QNAP HW JBOD|xfs|151

### Write Latency

Config | FileSystem | Speed (KB/s)
---|---|---
Individual|ext4|10.3
Individual|xfs|13.5
QNAP HW RAID 0|ext4|7.2
QNAP HW RAID 0|xfs|8.4
QNAP HW JBOD|ext4|29.4
QNAP HW JBOD|xfs|44.4

### Read throughput

Config | FileSystem | Speed (MB/s)
---|---|---
Individual|ext4|147.30
Individual|xfs|162.70
QNAP HW RAID 0|ext4|228.13
QNAP HW RAID 0|xfs|250.43
QNAP HW JBOD|ext4|155.32
QNAP HW JBOD|xfs|157.68
