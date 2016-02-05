# LogRecorder
Record system or application log to sdcard on Android device.

# Usage
直接复制 [LogRecorder.java](https://github.com/dxjia/LogRecorder/blob/master/LogRecorder.java) 文件到你的工程中，使用方式如下：
<br>首先在`AndroidManifest.xml`中增加权限：
```
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_LOGS" />
```

然后在代码中合适的地方使用，之后Log就会自动开始记录，直到调用`logRecorder.stop()`，或者进程结束：
```
	LogRecorder logRecorder
			 = new LogRecorder.Builder(context)
	               .setLogFolderName("foldername")
	               .setLogFolderPath("/sdcard/foldername")
	               .setLogFileNameSuffix("filesuffix")
	               .setLogFileSizeLimitation(256)
	               .setLogLevel(4)
	               .addLogFilterTag("ActivityManager")
	               .setPID(android.os.Process.myPid())
	               .build();

	logRecorder.start();
```

## setLogFolderName()
> 设定log输出目录名，如果该值与folder path都没有设定的话，会默认使用应用包名在sdcard下新建目录。

## setLogFolderPath()
> 设置Log输出目录绝对路径，该值会优先使用，会忽略folder name的设置。

## setLogFileNameSuffix()
> log文件名前缀，文件名会使用时间的形式，该值的设定会自动追加在时间之前，如setLogFileNameSuffix("mylog") 则最后的文件名为`mylog-2016-02-04-12-26-53.log`

## setLogFileSizeLimitation()
> 单个log文件的大小限制，超过设置的限制时，会自动新起新的文件记录log，**`注意`**: 是以`KB`为单位的。

## setLogLevel()
> 设置记录的log级别，默认2<br>
>   2 = verbose <br>
>   3 = debug <br>
>   4 = info <br>
>   5 = warning <br>
>   6 = error <br>
>   7 = silent(不输出任何log)

## addLogFilterTag()
> 设置log过滤的tag，可以add多个，如`addLogFilterTag("ActivityManager")`表示只过滤“ActivityManager”的log 

## setPID()
> 通过该方法可以指定一个特定的进程的log，如通过`setPID(android.os.Process.myPid())` 即可只输出自己的APP的log。
