
# define
tag: app_name
msg: message log

# log_level
--- user level ---
1.  msglog_v(tag,msg):  verbose
2.  msglog_d(tag,msg):  debug
3.  msglog_i(tag,msg):  infomation   

--- system level ---   
4.  msglog_w(tag,msg):  warn   
5.  msglog_e(tag,msg):  error  
6.1 msglog_a(tag,msg):  assert  
6.2 msglog_wtf(tag,msg):    what a terrible failure(alias function of assert)  

# log destination
Bit flag config to set log destination, config per tag per log_level
## bit flag values
- stdout: debug print 
- stderr: debug print 
- local log file by date
- udp server(future task, no need to implement now)
- ... (future task, no need to implement now)
## default config
- msglog_v: stdout
- msglog_d: stderr
- msglog_i: stderr | local log file by date
- msglog_w: stdout
- msglog_e: stderr
- msglog_a: stderr | local log file by date

# server apps
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

# client
- register by tag

# log pattern
## detail
 1.tag: tag
 2.lvl: log level 
 3.utime: unix time
 4.msg: log message

## example log
```
$ cat 20170629.log
{"tag":"appname1","lvl":"v","utime":"1498726192","msg":"this is log message1..."},
{"tag":"appname2","lvl":"d","utime":"1498726195","msg":"this is log message2..."},
{"tag":"appname1","lvl":"w","utime":"1498726196","msg":"this is log message3..."},
{"tag":"appname1","lvl":"a","utime":"1498726199","msg":"this is log message4..."},
$
```

Note that you can use json array `[]` for json loading, for example,   
```
mylog = [
{"tag":"appname1","lvl":"v","utime":"1498726192","msg":"this is log message1..."},
{"tag":"appname1","lvl":"a","utime":"1498726199","msg":"this is log message4..."},
]
```  
