## 任务结果分配

查看任务的分配情况

**URL**
```  
http://api.crowdtask.cn/api/task/assignments
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
|signature|是|string|**header**|身份签名，[计算方法](../api/index.md#signature)|
|taskid|是|string|parameter|创建项目后返回的任务ID|

**返回值示例**
```
{
	"taskid":"RExJuKBcyQgEtIec",						// 任务ID
	"maxassignments":2,									// 最大可分配数（需要多个不同工人来完成同一个任务）
	"numberofassignmentsavailable":0,					// 剩余的可分配任务数
	"numberofassignmentsfinished":2,					// 已执行的任务数量	
	"assignmentid":[									// 任务分配ID
		"mgCmOBuDGYosiFtM",
		"WjCwVWYyTQinBWbN"
	]
}
```


## 单个任务结果

查看任务单个结果的详细信息

**URL**
```  
http://api.crowdtask.cn/api/task/assignment
```
   
**HTTP请求方式**
```
GET
```

**参数说明**

|参数名|必须|参数类型|参数位置|参数说明|
|:---|:---|:---|:---|:---|
|accessid|是|string|**header**|访问授权秘钥ID，用户可在后台查看|
|localtime|是|string|**header**|本地时间('1970-01-01 00:00:00' GMT之后的毫秒数)|
|signature|是|string|**header**|身份签名，[计算方法](../api/index.md#signature)|
|assignmentid|是|string|parameter|任务分配ID|

**返回值示例**
```
{		
	"assignmentid":"mgCmOBuDGYosiFtM",					// 任务分配ID
	"workerid":123,										// 工人ID
	"assigntime":,										// 分配时间('1970-01-01 00:00:00' GMT之后的毫秒数)
	"answertime":,										// 提交答案时间('1970-01-01 00:00:00' GMT之后的毫秒数)
	"answer":"input_1:kitch;input_2:bedroom;input_3:bedroom"
														// 答案，多个输入项以';'分割，每个输入项的名字和值以':'分割
														// 如果答案还没提交，answer为null，answertime为0
}
```