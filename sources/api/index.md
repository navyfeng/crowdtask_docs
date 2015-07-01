
## API 的请求格式

所有的API支持HTTP协议，具体的请求格式如下：

`http://api.crowdtask.cn` + action_uri

- - -

## API 的响应格式

如果API调用成功，返回的Http状态码等于200，Http响应结果包含了请求的结果

如果API调用失败，返回的Http状态码为40x或50x，Http响应结果包含了失败原因

Http响应结果都是JSON格式，返回的信息示例如下: 
```
    # 请求成功，Http状态码为200
    {
		...
    }

    # 请求失败，Http状态码为40x或50x
    {
        "status": 40x|50x,
        "reason": "error description"
    }
```
- - -

## 公共参数
|参数名|必须|参数类型|参数位置|参数说明|
|----|------|------|------|------|
|accessid|是|string|**header**|访问授权秘钥ID|
|localtime|是|string|**header**|本地时间，unix_timestamp('1970-01-01 00:00:00' GMT之后的毫秒数)|
|signature|是|string|**header**|[签名](#signature)|


##signature

所有API调用时需要附带签名（signature）参数，用来进行身份校验

accessid和accesssecreykey用户注册时生成的一对字符串，其中accesssecreykey用作计算签名，accessid用作请求参数

签名的计算方式如下:
```
data = action_uri+'&'+localtime
signature = hex_hmac_md5(accesssecretkey,data)

```
举例如下: 

``` 
action_uri='/api/task/batch'  
localtime='1435132361000'
accesssecretkey='0987654321'
data='/api/task/batch&1435132361000'
signature='6c52e7babb792123c66424d36c7805ba'
```
- - -

