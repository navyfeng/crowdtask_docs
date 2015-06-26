    
用户举报的垃圾邮件, 此用户的地址会进入垃圾举报列表. 

在此列表中的邮件地址, 都不会再被发送邮件.

你可以对此列表进行查询操作.
     
- - -
##查询
     
**URL**
```  
https://sendcloud.sohu.com/webapi/spamReported.get.json
```
   
**HTTP请求方式**   
```bash
post    get
```
    
**参数说明**
    
|参数|类型|必须|说明|    
|:---|:---|:---|:---|
|api_user|string|是|子账号|
|api_key|string|是|密码|
|days|int|*|过去 days 天内的统计数据 (`days=1`表示今天)| 
|start_date|string|*|开始日期, 格式为`yyyy-MM-dd`|
|end_date|string|*|结束日期, 格式为`yyyy-MM-dd`|
|email|string|*|查询该地址在举报列表中的详情|
|start|int|否|查询起始位置, 取值区间 [0-], 默认为 0|
|limit|int|否|查询个数, 取值区间 [0-100], 默认为 100|

提示:

1. 如果指定时间区间, 则是查询此时间区间内的举报列表. 注意: **start_date 与 end_date 的组合** 或者 **days 参数**, 二者取一. 
2. 如果指定email, 则是查询此地址在举报列表中的详细信息. 注意: 此时, 时间区间参数失效.


请求示例:    
```
http://sendcloud.sohu.com/webapi/spamReported.get.json?api_user=***&api_key=***
```
    
**返回值说明**
    
无    
    
**返回值示例**    
```
{
    "message": "success",
    "bounces": [
        {
            "email": "123@qq.com",
            "reason": "spam reported",
            "create_at": "2014-11-10 18:26:30"
        }
    ]
}
```

