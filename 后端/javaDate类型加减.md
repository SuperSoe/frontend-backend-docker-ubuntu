## java的ｄａｔｅ类型简单运算#
### 1.


```
Calendar fromDate = Calendar.getInstance();
fromDate.setTime(wifiConnectInfo.getConnectTime());                   
fromDate.add(Calendar.HOUR, -1);
```