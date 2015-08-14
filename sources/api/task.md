
## 创建

**URL**
```
http://api.crowdtask.cn/api/task/batch
```
   
**HTTP请求方式**
```
POST
```

**参数说明**

|参数名|必须|参数类型|参数位置|参数说明|
|:---|:---|:---|:---|:---|
|accessid|是|string|**header**|访问授权秘钥ID，用户在后台查看|
|localtime|是|string|**header**|本地时间，unix_timestamp('1970-01-01 00:00:00'GMT之后的秒数)|
|signature|是|string|**header**|[身份签名](../api/index.md#signature)|
|projectid|是|string|parameter|常规项目ID|  
|taskinputcvs|是|file|parameter|[常规CVS文件](../api/index.md#cvs)|  
|publish|否|boolean|parameter|创建后是否立即发布，默认为true|  

注意:

1. accessid、localtime、signature必须添加在HTTP请求的头部
2. 输入的CVS文件必须为UTF-8编码
3. localtime和服务器的时间相差不能超过5分钟
4. taskinputcvs中包含的任务行数不能超过100，超过部分将会被丢弃

**返回值示例**
```
{
	"tasknum":3,					// 成功创建的任务数量
    "batchSN":"SCTBBWKwHZDcNedo",	// 任务批次号
    "taskids":[						
        "yqELGfLUvRzsIYPe",			// 任务ID
		"RExJuKBcyQgEtIec",
		"ACfCzYjpLJyeiMAL"
    ]
}
```


## 查看

**URL**
```  
http://api.crowdtask.cn/api/task/details
```
   
**HTTP请求方式**
```
GET
```

**参数说明**

|参数名|必须|参数类型|参数位置|参数说明|
|:---|:---|:---|:---|:---|
|accessid|是|string|**header**|访问授权秘钥ID，用户可在后台查看|
|localtime|是|string|**header**|本地时间，unix_timestamp('1970-01-01 00:00:00' GMT之后的毫秒数)|
|signature|是|string|**header**|[身份签名](../api/index.md#signature)|
|taskid|是|string|parameter|创建项目后返回的任务ID|  

**返回值示例**
```
{
	"projectid":"IHLSGgcyQgEpxwxl",						// 所属项目ID
	"taskid":"RExJuKBcyQgEtIec",						// 任务ID
	"title":"家居图片分类",								// 标题
    "description":"为你看到的3张图片选择合适的分类，图片可能是卧室、厨房、书房等，如果是非室内图片请选择类型为其他，并填写一个合适的标签",
														// 任务描述
	"keywords":"图片,分类,家居",						// 任务关键字
	"reward":20,										// 酬金
	"lifetimeinseconds":1800,							// 有效期（秒）
	"maxassignments":1,									// 最大可执行数（需要几个不同工人来完成同一个任务）
	"numberofassignmentsavailable":1,					// 剩余的可执行任务数
	"numberofassignmentsfinished":0,					// 已执行的任务数量
	"createtime":1435132361000							// 任务创建时间(毫秒，'1970-01-01 00:00:00' GMT之后的毫秒数)
	"expiration":1435132361000,							// 任务过期时间(毫秒，'1970-01-01 00:00:00' GMT之后的毫秒数)
	"autoapprovaldelayinseconds":604800,				// 酬金支付时限（秒）
	"assignmentdurationinseconds":120,					// 任务执行时限（秒）
    "question":"mydomain.com/img/4.jpg mydomain.com/img/5.jpg mydomain.com/img/6.jpg"
														// 上传的变量值（cvs文件的一行）
}
```



