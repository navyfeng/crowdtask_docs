
## API请求格式

所有的API支持HTTP协议，具体的请求格式如下：

`http://api.crowdtask.cn` + action_uri

- - -

## API响应格式

如果API调用成功，返回的Http状态码为20x，Http响应结果包含了请求的结果

如果API调用失败，返回的Http状态码为40x或50x，Http响应结果包含了失败原因

Http响应结果都是JSON格式，返回的信息示例如下: 
```
    # 请求成功，Http状态码为20x
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

## API公共参数
|参数名|必须|参数类型|参数位置|参数说明|
|----|------|------|------|------|
|accessid|是|string|**header**|访问授权秘钥ID|
|localtime|是|string|**header**|本地时间，unix_timestamp('1970-01-01 00:00:00' GMT之后的毫秒数)|
|signature|是|string|**header**|[API签名](#API签名)|


## API签名

所有API调用时需要附带签名（signature）参数，用来进行身份校验

accessid和accesssecreykey用户注册时生成的一对字符串，其中accesssecreykey用作计算签名，accessid用作请求参数

签名的计算方式如下:
```
data = action_uri+'&'+localtime
signature = hex_hmac_md5(accesssecretkey,data)

```
签名示例: 

``` 
action_uri='/api/task/batch'
localtime='1435132361000'
accesssecretkey='0987654321'
data='/api/task/batch&1435132361000'
signature='6c52e7babb792123c66424d36c7805ba'
```
- - -


## 常规JSON文件

常规JSON文件是用户批量导入常规任务时需要上传的文件

它包括了任务模板中各个变量的值，格式如下：

**示例**

```
[
	{
		"img_url_1":"http://crowdtask.oss-cn-hangzhou.aliyuncs.com/0.png",		// 模板变量img_url_1的值
		"img_url_2":"http://crowdtask.oss-cn-hangzhou.aliyuncs.com/1.png"		// 模板变量img_url_2的值
	},
	{
		"img_url_1":"http://crowdtask.oss-cn-hangzhou.aliyuncs.com/2.png",
		"img_url_2":"http://crowdtask.oss-cn-hangzhou.aliyuncs.com/3.png"
	}
]

```
>[常规JSON文件示例](/resource/sample.json)

**注意:** 常规任务的JSON文件必须是UTF8编码


## 训练JSON文件

训练JSON文件是用户批量导入训练任务时需要上传的文件

它包括了任务模板中各个变量的值、参考答案、检验方式，格式如下：

**示例**

```
[
	{
		"img_url_1":"http://crowdtask.oss-cn-hangzhou.aliyuncs.com/0.png",		// 模板变量img_url_1的值
		"img_url_2":"http://crowdtask.oss-cn-hangzhou.aliyuncs.com/1.png"		// 模板变量img_url_2的值
		"$answers":{
			"input_1":1,		// 输入项input_1的参考答案为1
			"input_2":2			// 输入项input_2的参考答案为2
		},
		"$validators":[
			{	// 答案正确的标准为输入项input_1的值等于1
				"name":"input_1",		
				"comparator":"equals",
				"value":,1
			},
			{	// 答案正确的标准为输入项input_2的值大于1
				"name":"input_2",
				"comparator":"bigthan",
				"value":,1
			}
		]
	},
	{
		"img_url":"http://crowdtask.oss-cn-hangzhou.aliyuncs.com/2.png",
		"img_url":"http://crowdtask.oss-cn-hangzhou.aliyuncs.com/3.png",
		"$answers":{
			"input_1":1,
			"input_2":2
		},
		"$validators":[
			{
				"name":"input_1",
				"comparator":"equals",
				"value":,1
			},
			{
				"name":"input_2",
				"comparator":"bigthan",
				"value":,2
			}
		]
	}
]


```
>[训练JSON文件示例](/resource/trainingtask.json)

**注意:** 训练任务的JSON文件必须是UTF8编码

## 常规CVS文件

常规CVS文件是用户批量导入常规任务时需要上传的文件

它包括了任务模板中各个变量的值，格式如下：

| variable_1 | variable_2| variable_3 |
| ------------ | ------------- | ------------ |
| value_1 | value_2 | value_3 |
| value_4 | value_5 | value_6 |

>第一行是变量名，从第二行开始是变量值，[常规CVS文件示例](/resource/sample.cvs)

**注意:** 常规任务的CVS文件必须是UTF8编码，变量名和值都不能包含空格


## 训练CVS文件

训练CVS文件是用户批量导入训练任务时需要上传的文件

和常规任务的CVS文件相比，它不仅包括了任务模板中各个变量的值，而且包括了输入项的参考答案和计分准则,格式如下：

| variable_1 | variable_2| variable_3 | $input_1 | $input_2 | $validator|
| ------------ | ------------- | ------------ |------------ |------------ |------------ |
| value_1 | value_2 | value_3 |input_value_1|input_value_2|input_1#equals#1;input_2#biggerThan#3|
| value_4 | value_5 | value_6 |input_value_3|input_value_4|input_1#noEquals#2;input_2#lessThan#4|

>第一行是变量名
>第二行开始是变量值、参考答案、计分准则，[训练CVS文件示例](/resource/trainingsample.cvs)

**注意:** 常规任务的CVS文件必须是UTF8编码，变量名和值都不能包含空格


