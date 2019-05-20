##### Timer

###### 事件

```c#
private void timer_Tick(object sender, EventArgs e)
{
    SysTime.Text = DateTime.Now.ToString("yyyy-MM-dd hh:mm:ss");  // 12小时制
    SysTime.Text = DateTime.Now.ToString("yyyy-MM-dd HH:mm:ss");  // 24小时制
}
```

**注：MM-月，mm-分钟**

###### 初始化显示世间

```
timer.Interval = 1000;  // 1000毫秒
timer.Start();
```

###### 时间换算

```
获取或之前设置的时间，以毫秒为单位， Tick 事件引发的最后一个匹配项相对 Tick 事件。
1秒=1000毫秒(ms)
1毫秒=1／1,000秒(s)
1秒=1,000,000 微秒(μs)
1微秒=1／1,000,000秒(s)
```

