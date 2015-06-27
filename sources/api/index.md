
## API 的请求格式

`http://api.crowdtask.cn/action_uri`

所有的API的调用都要附带用户的签名，具体计算签名的计算方法如下：

>localtime，本地时间，1900-01-01 00:00:00到现在的秒数，必须和服务器时间相差小于15分钟
>signature=hmac(action_uri+'&'+localtime+'&'+accesssecretkey)

>

>例如uri=

不同的API有不同的参数以及调用方法（GET|POST）

**提示**: 所有的 API 都支持 HTTPS. 
- - -

## API 的响应格式

如果API调用成功，返回的HttpStatus等于20x，Http响应结果包含了请求的结果

如果API调用失败，返回的HttpStatus为40x或50x，Http响应结果包含了失败原因

Http响应结果都是JSON格式，返回的信息示例如下: 
```
    # 请求成功
    {
        "status": "success",
		"result":{
			...
		}
    }

    # 请求失败
    {
        "status": "error",
        "reason": "error description"
    }
```
- - -

## accessId 和 accesssecretkey

accessid和accesssecreykey是接口调用时必须要使用的一对秘钥，在调用API时用来计算签名（signature）进行身份校验。


两者的计算关系如下:
```
to = [A, B, C]
emailId_A = messageId + to.index(A) + '$' + A
emailId_B = messageId + to.index(B) + '$' + B
emailId_C = messageId + to.index(C) + '$' + C

# 注意: position 不做位数补齐
```
举例如下: 
```
# to = ["ben@ifaxin.com", "joe@ifaxin.com", "bida@ifaxin.com", ... , "lianzimi@ifaxin.com"]
1425758592214_4576_32113_9310.sc-10_10_127_105-inbound  # messageId
1425758592214_4576_32113_9310.sc-10_10_127_105-inbound0$ben@ifaxin.com  # emailId
1425758592214_4576_32113_9310.sc-10_10_127_105-inbound1$joe@ifaxin.com  # emailId
1425758592214_4576_32113_9310.sc-10_10_127_105-inbound2$bida@ifaxin.com  # emailId
...
1425758592214_4576_32113_9310.sc-10_10_127_105-inbound99$lianzimi@ifaxin.com  # emailId
```
- - -

##CVS文件
CVS文件是用户批量导入任务时需要上传的文件。它包括了任务模板中各个变量的值，格式如下：

>variable_1 variable_2 	variable_3 ...

>value_1 	value_2 	value_3 ...

>value_4 	value_5 	value_6 ...

实际例子

>img_url_1 img_url_2 imag_url_3 input_init_value_1

>mydomain.com/img/1.jpg mydomain.com/img/2.jpg mydomain.com/img/3.jpg  abc

>mydomain.com/img/4.jpg mydomain.com/img/5.jpg mydomain.com/img/6.jpg  def

**注意:** 如果变量的值中包含了空格，请用将值用""进行包含;如果值中包含了"，请转义成\"

>img_url_1 img_url_2 imag_url_3 input_init_value_1

>mydomain.com/img/1.jpg mydomain.com/img/2.jpg mydomain.com/img/3.jpg  "abc = 123"

>mydomain.com/img/1.jpg mydomain.com/img/2.jpg mydomain.com/img/3.jpg  def="123"

