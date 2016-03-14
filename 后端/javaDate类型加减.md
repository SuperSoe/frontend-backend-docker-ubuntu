## java的ｄａｔｅ类型简单运算#
### 1.


```
Calendar fromDate = Calendar.getInstance();
fromDate.setTime(wifiConnectInfo.getConnectTime());                   
fromDate.add(Calendar.HOUR, -1);
```

### 2.
```
     ZonedDateTime now = ZonedDateTime.now();
     
     wifiService.findExistingWifiUserByDates(Date.from(now.minusHours(1).toInstant()), Date.from(now.toInstant()));

```