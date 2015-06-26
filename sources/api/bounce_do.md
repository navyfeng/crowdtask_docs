    
由特定原因(如地址不存在等)被退信的邮件会进入此列表.

在此列表中的邮件地址, 都不会再被发送邮件.
    
你可以对此列表进行查询, 删除操作
    
- - -
##查询    
    
**URL**    
```
http://sendcloud.sohu.com/webapi/bounces.get.json
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
|email|string|*|查询该地址在退信列表中的详情|
|start|int|否|查询起始位置, 取值区间 [0-], 默认为 0|
|limit|int|否|查询个数, 取值区间 [0-100], 默认为 100|

提示:

1. 如果指定时间区间, 则是查询此时间区间内的退信列表. 注意: **start_date 与 end_date 的组合** 或者 **days 参数**, 二者取一. 
2. 如果指定email, 则是查询此地址在退信列表中的详细信息. 注意: 此时, 时间区间参数失效.

请求示例:
```
http://sendcloud.sohu.com/webapi/bounces.get.json?api_user=***&api_key=***&days=100&start=0

http://sendcloud.sohu.com/webapi/bounces.get.json?api_user=***&api_key=***&email=***
```
    
**返回值说明**
    
|参数|说明|
|:---|:---|
|email|邮件地址|
|reason|退信原因|
|create_at|退信时间|
    
**返回值示例** 
```    
{
    "message":"success",
    "bounces":[{"email":"109509759@qq.com","reason":"Mailbox not found. http://service.mail.qq.com/cgi-bin/help?subtype=1&&id=20022&&no=1000728","create_at":"2015-03-12 19:07:40"}]
}  
```
    
- - -
    
##删除

**URL**    
```
http://sendcloud.sohu.com/webapi/bounces.delete.json
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
|start_date|string|*|开始日期, 格式为`yyyy-MM-dd`|
|end_date|string|*|结束日期, 格式为`yyyy-MM-dd`|
|email|string|否|要删除的地址|
    
提示:

1. 如果指定时间区间, 则是删除此时间区间内的所有退信地址.
2. 如果指定email, 则是在退信列表中删除此地址. 注意: 此时, 时间区间参数失效.
    
**请求示例**
```
http://sendcloud.sohu.com/webapi/bounces.delete.json?api_user=***&api_key=***&email=***
```
    
**返回值说明**
    
|参数|说明|
|:---|:---|
|del_count|成功删除的地址个数|
    
**返回值示例**
```
{
    "message":"success",
    "del_count":1
}
```    
- - -
    
##计数

**URL**
```
http://sendcloud.sohu.com/webapi/bounces.count.json
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
    
提示:

1. 获取数据时, 必须指定时间区间. 即 **start_date 与 end_date 的组合** 或者 **days 参数**, 需二者取一
    
**请求示例**
```
http://sendcloud.sohu.com/webapi/bounces.count.json?api_user=***&api_key=***&days=10
```
    
**返回值说明**
    
|参数|说明|
|:---|:---|
|count|地址数量|
    
**返回值示例**
```
{
    "message":"success",
    "count":200
}
```

