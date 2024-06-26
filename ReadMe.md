### Unity CacheServer Cluster
# Uses nodejs cluster feature to start cache server for multiple workers.
Based on cache server version 5.3  
Should work for Unity AssetDatabase v1, does not support Unity versions priorior 5.0.  
This feature is useful for huge amount of team to collaborate with the same cache server for huge projects.  
Will allocate workers per 16GB of memory. Recommend to deploy it to a large ram and large SSD disk space machine.  
Recommend to run it on linux rather than windows (but windows should work).  
The cluster version of cache server WON'T try to delete old cache or free space because it might conflict to do so using workers.  
However, it used to removes old cache based on file's access time. You may try to remove old cache using external tool or by bash.  

For example (delete cache files who has not been visited for more than 200 days. Please make sure your OS has enabled file's access time updating by reading.):

``` bash
cd ${Path_To_Cache_Dir}
find . -atime +200 -delete -type f
```

Launch CacheServer example:
``` bash
${Path_To_Nodejs} main.js --path ${Path_To_Cache_Dir} > ${Path_To_Log_File}.log
```

Tested on tlinux 2.2 (like CentOS 7.9 based on linux kernel 3.10.107) with nodejs v0.12.7, E5-2670v3 with 128GB of memory, and more than 2TB of cache with more than 100 people of team.  
Recommend to use the same version as me, tried on node 16 and looks like node 16 is significantly slower than node v0.12.7.  
