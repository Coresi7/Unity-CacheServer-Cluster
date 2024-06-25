### Unity CacheServer Cluster
# Uses nodejs cluster feature to start cache server for multiple workers.
Based on cache server version 5.3  
Should work for Unity AssetDatabase v1, does not support Unity versions priorior 5.0.  
This feature is useful for huge amount of team to collaborate with the same cache server for huge projects.  
Recommend to run it on linux rather than windows (but windows should work).  
Cluster version of cache server won't try to delete old cache or free space because it might conflict to do so using workers.  
However, it used to removes old cache based on file's access time. You may try to remove old cache using external tool or by bash.  

For example:

``` bash
cd ${Path_To_Cache_Dir}
find . -atime +200 -delete -type f
```

Launch CacheServer example:
``` bash
${Path_To_Nodejs} main.js --path ${Path_To_Cache_Dir} > ${Path_To_Log_File}.log
```