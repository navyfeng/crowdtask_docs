
## 流程

* 用户在前台创建项目（设计任务模板,设置过滤条件、酬金、超时时间等）

* 用户编写程序, 调用接口向已创建好的项目中批量导入任务

* CrowdTask将任务分发给工人进行处理 ( 排队调度, 变量替换, 结果反馈 )

* 在整个处理过程中，用户可以调用接口监控项目的整体执行情况

* 如果项目设置了notify_url,平台将主动通知用户获取任务的处理结果

* 如果项目没有设置notify_url,用户需要调用接口轮询获取任务的处理结果

------

## 项目

在发布任务前，用户需要创建一个项目，用来描述任务的基本信息、任务内容等。任务的基本信息包括标题、任务说明、关键字、酬金等，任务内容是以HTML格式组织的网页。


**训练项目**: 训练项目是针对某些难度较大或需要一定专业技能的任务设置的前置项目。工人只有通过训练项目的考核才可以接取指定的任务

注意: 如果项目的内容可能涉及成人内容，请在创建项目时标记。

------

## 任务模板

在创建项目时，用户可以设计个性的模板（HTML）来表达任务的内容。任务模板中包含了变量、输入项。例如一个图片分类的项目，它的任务模板可能包含了一个图片地址的变量，以及一个分类结果的输入项。

在发布任务时，用户上传实际的图片地址，任务模板经过变量替换之后即可生成一个完整的任务页面。工人得到任务页面后，完成输入项的输入后，将结果提交至后台。

* 在任务模板中可以加入js脚本，便于处理一些简单业务逻辑

------

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





