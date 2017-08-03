
# Define
tag: app_name
msg: message log

# Init function
```
cfg = new_msglog("tag_name");
```

# Log_level  
1.  Verbose  
     msglog_v(cfg, msg)        
2.  Debug  
     msglog_d(cfg, msg)        
3.  Information     
     msglog_i(cfg, msg) 
4.  Warn  
     msglog_w(cfg, msg)     
5.  Error  
     msglog_e(cfg, msg)     
6.  Assert  
     6.1 msglog_a(cfg, msg)      assert  
     6.2 msglog_wtf(cfg, msg):   what a terrible failure(alias function of assert)  

# Log destination
Bit flag config to set log destination, config per tag per log_level  
## Bit flag values
- stdout: debug print  
- stderr: debug print  
- local log file by date  
- udp server(future task, no need to implement now)  
- ... (future task, no need to implement now)  
## Default config
- msglog_v: stdout  
- msglog_d: stderr  
- msglog_i: stdout | local log file by date  
- msglog_w: stdout  
- msglog_e: stderr  
- msglog_a: stderr | local log file by date  

# Server apps
- list all tag   
- list all destination config by tag  
- set destination by tag and log_level 
- save local log file by date  
    + init_func(root_locallog_path)  
- list local log files  
- cat local log files by date  
- auto remove local logs older than 30 days  
- for destination stderr  
 + enable/disable by tag (default disable)  
- support udp(future task)  

## To show
- all(no filter)  
- filter by tag  
+ show by level  

# Client
- register by tag  

# Log pattern
## Detail
 1.tag: tag  
 2.lvl: log level   
 3.utime: unix time  
 4.msg: log message  

## Example log
```
$ cat 20170629.log
{"tag":"appname1","lvl":"v","utime":"1498726192","msg":"this is log message1..."},
{"tag":"appname2","lvl":"d","utime":"1498726195","msg":"this is log message2..."},
{"tag":"appname1","lvl":"w","utime":"1498726196","msg":"this is log message3..."},
{"tag":"appname1","lvl":"a","utime":"1498726199","msg":"this is log message4..."},
$
```

## Trick: For javascript loading data, you may use json array `[]`, e.g.,    
```
mylog = [
{"tag":"appname1","lvl":"v","utime":"1498726192","msg":"this is log message1..."},
{"tag":"appname1","lvl":"a","utime":"1498726199","msg":"this is log message4..."},
]
```  
