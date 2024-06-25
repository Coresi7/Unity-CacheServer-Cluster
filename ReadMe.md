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

You may change workers number in CacheServer.js's Start method.  
Recommend to start 1 worker per 16GB of memory. For example, if you have 128GB ram, try to start 8 workers.
``` js
exports.Start = function(a_cacheSize, a_port, a_path, a_logFn, a_errCallback)
{
    // codes...
    for (var i = 0; i < 2; i++) // start only 2 nodes for test. Change this number to fit you well.
    {
        cluster.fork();
    }
    // codes...
}
```