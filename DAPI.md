 
**接口调用文档**

Author:  [Linkenpeng](mailto:collin_linken@qq.com)

[前言](#前言)

* 第一部分 [下行接口部分](#下行接口部分)
	* 1．1、	[获得周边小区接口](#获得周边小区接口)
	* 1．2、	[广告接口](#广告接口)
	* 1．3、	[动态列表接口](#动态列表接口)
	* 1．4、	[吐槽详情接口](#吐槽详情接口)
	* 1．5、	[获得分类接口](#获得分类接口)
	* 1．6、	[圈子吐槽接口](#圈子吐槽接口)
	* 1．7、	[圈子列表接口](#圈子列表接口)
	* 1．8、	[圈子帖子列表接口](#圈子帖子列表接口)
	* 1．9、	[评论列表接口](#评论列表接口)
	* 1．10、[个人空间接口](#个人空间接口)
	* 1．11、[对话列表接口](#对话列表接口)
	* 1．12、[对话详情接口](#对话详情接口)
	* 1．13、[通知列表接口](#通知列表接口)
	* 1．14、[个人设置读取接口](#个人设置读取接口)
	* 1．15、[好友列表接口](#好友列表接口)
	* 1．16、[好友添加申请列表接口](#好友添加申请列表接口)
	
	
* 第二部分 [上行接口部分](#上行接口部分)
	* 2.1、	[注册获取验证码接口](#注册获取验证码接口)
	* 2.2、	[注册接口](#注册接口)
	* 2.3、 [普通登录接口](#普通登录接口)
	* 2.4、	[第三方登录接口](#第三方登录接口)
	* 2.5、	[找回密码接口](#找回密码接口)
	* 2.6、	[退出登录接口](#退出登录接口)
	
	
 
<h2>前言</h2>  

本接口调用文档，旨在告诉客户端如何调用服务器请求，从而实现客户端的所有业务逻辑。
下行接口：根据客户端发起的请求，网站服务端进行业务逻辑的操作之后，然后通过接口返回客户端所需要的各种图文数据; 
上行接口：如果客户端所要发起的操作，是需要触发服务端进行系统业务逻辑操作，或者进行数据增删改等操作的时候,会通过上行接口将客户端的请求，送达给服务器，并在后台进行相应的业务逻辑操作,最后将获得相应的返回值以及是否操作成功的标记。

注：

	1)	下行接口中，除非标注有POST方式，否则一律用GET方式请求数据。  
	2)	上行接口中，除非标注有GET方式，否则一律用POST方式发送数据。  
	3)	在上行接口中，包含有部分下行接口，用来生成发布界面，如：空间列表，和谁在一起。  
	4)	如果服务器返回：
		"data": {
			"return": "-1",
		},
		"msgkey": "auth_failure",
		"msg": "auth_failure",
		"error": 1
		则代表m_auth不对或者已经失效，需要重新登录更新m_auth。  

所有的接口服务器均以Json格式返回数据，在每个返回的信息中，分别是：   
>  

	data: 	下行接口中代表客户端真正需要的数据。  
	msgkey: 代表服务器针对该次请求的信息提示key，客户端可以根据此信息自己再定义信息。  
	msg: 	代表服务器针对该次请求的辅助信息提示。  
	error: 	代表是否获取数据错误状态， 1 失败， 0成功。  
	
返回的数据示例：

>  

	{

		"data": {
			"adid": "2",
			"title": "手机广告",
			"imagesrc": "http://www.baidu.com/img/baidu_sylogo1.gif",
			"idtype": "blog",
			"id": "1"
		},
		"msgkey": "rest_success",
		"msg": "数据获取成功",
		"error": 0
	}


注：开发的时候如果想方便的查看每个接口的返回信息，可以在url中增加一个debug=1的参数，如：
网站域名/dapi/info.php?ac=ad&debug=1
若没有此参数，将返回json数据格式。


<h2>第一部分</h2> <h2>下行接口部分</h2>

<h3>1.1、</h3><h3>广告接口</h3>  
【参数】  
无  
【调用方式】  
网站域名/dapi/info.php?ac=ad  
【返回值】  
> 

	title		广告标题  
	imagesrc	广告图片url  
	idtype		广告对应的帖子类型  
	id			帖子id

 
<h3>1.2、</h3><h3>今日话题</h3>  
【参数】   
>   

	topicid:	指定的话题id【默认为空，取今天的话题】
	perpage: 	分页大小， 默认10 
	page:		当前页 
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	
【调用方式】  
网站域名/dapi/space.php?do=topic&m_auth=?   
【返回值】  
>  

	subject:			标题
	message:			内容
	dateline:			发布时间
	endtime：			结束时间
	pic:				今日话题图片
	imagesize
		height:			图片高度
		width:			图片宽度
	nexttopicid:		下一话题id【当前话题还有帖子未看完时为空；如果当前帖子已经看完，则会返回下一个话题的id，客户端需要利用这个id重新请求一次话题接口得到下一话题的内容】
	content: 【话题的内容】	 
		image_1：   内容的图片 
		idtype：    内容的类型(blogid,eventid,videoid,photoid) 
		id：        内容的id 
		uid：  	    发布人的uid 
		name：  	发布人的昵称 
		subject：   内容的标题 
		message：   内容的详情说明 
		imagesize： 图片的尺寸 
			height：高 
			width： 宽 
		commentlist【评论】
			authorid:		评论用户uid
			avatar:			头像url
			vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
			authorname:		评论用户名
			note:			关系备注
			message:		评论内容
			dateline:		评论时间
			lng:			经度
			lat:			纬度
			address:		地名
			come:			发布来源	
 
<h3>1．3、	</h3><h3>家庭动态列表接口</h3>  
【参数】  
>  

	do:	 		home
	uid:		用户id, 无则代表登陆用户的uid  
	perpage: 	分页大小， 默认10
	page:		当前页
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	idtype:		动态的类型【可选】，默认为空（代表全部），如果指定值（则只得到该类型的动态）
	apptype:	默认为空[显示全部类型的动态], 设为pm[则去掉评论以及行为动态]
	date:		指定日期的动态，格式: 2013-08-01
【调用方式】  
网站域名/dapi/space.php?do=home&m_auth=?    
【返回值】  

>

	1）多维数组：  
		avatar: 		发布用户头像url
		vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
		name: 			用户昵称
		note : 			关系备注
		dateline: 		动态时间
		tag:
			tagid:		空间id
			tagname:	空间名称
		idtype: 		动态类型(
				eventid: 		发布活动
				reeventid：		转采活动
				eventcomment：	活动评论
				blogid: 	 	发布更新日志
				reblogid： 		转采日志
				blogcomment： 	日志评论
				photoid：	  	上传图片
				photocomment： 	评论图片
				rephotoid：		转采图片
				videoid：		发布视频
				revideoid：		转采视频
				videocomment：	视频评论
				profield: 		更新资料
				avatar:  		更新头像
		)
		replynum		评论数量
		reblognum		转发数量
		love			收藏数量
		picnum			照片数量
		mylove			是否是我收藏的，1：是，0：否
		eventdetail		活动详情   
        eventstarttime	活动时间  
	2）转采  
		fuid				原作者uid
		fname				原作者名称
	3)普通动态  
		title: 				动态标题
		image_1 – image_4:	动态带的图片和内容附图的数量, 如果有图片则有值，否则为空值
		image_1_width – image_4_width:		动态图片的宽度
		image_1_height – image_4_height:	动态图片的高度
		message:			动态简介文字
		id:					原文id
		fuid:				原文所属于的空间id
		fname:				原文所属于的空间名称
		fmessage:			原文内容
	4） 活动动态  
		lng:				活动地点的经度
		lat:				活动地点的纬度
		location:			活动地点的地名
	5） 行为动态
		
		普通的行为动态：
		uid:				行为人uid
		name:				行为人名字
		fuid:				对象人uid
		fname:				对象人名字
		
		评论的行为动态(即：idtype为：**comment的)：
		cuid:				评论人uid
		cname:				评论人名字
		cavatar: 			评论人头像
		cvipstatus:			personal: 个人, family： 家庭， 空值：普通用户
		uid:				被评论对象人uid
		name:				被评论对象人名字
		
		------------------------------
		subject：			被操作的对象名称
		id：				被操作的id
		idtype：			被操作的类型
		
	6) 发布渠道 
		come: 				发布的渠道  
	
	7） 最新的两条评论  
		comment： 	数组
			authorid：		评论人的uid
			authorname:		评论人的名字
			message：		评论内容
			dateline：		评论时间
		
		loveuser 收藏人列表(数组)
			uid				收藏人uid
			name			收藏人名字
			avatar			收藏人头像
			vipstatus		收藏人身份(personal: 个人, family： 家庭， 空值：普通用户)  

 
<h3>1．4、	</h3><h3>照片详情接口</h3>  
【参数】  
> 

	do:	 		photo
	uid: 		照片发布人的uid  
	id:	        照片帖子id  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=photo&id=293&m_auth=?&uid=?  
【返回值】  
>  

	1）
	uid:			发布者的uid
	name:			发布者的name
	avatar:			发布者的头像  
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	note:			关系备注
	dateline:		发布时间
	title:			标题
	tag:
		tagid:		空间id
		tagname:	空间名称
	2）转采
	fuid:			转采uid
	fname:			转采者名字
	3） 
	rephotonum：	转采数量
	replynum：		评论数量
	love:			收藏数量
	loveuser：		收藏人列表【多维数组】
		uid:		收藏人的uid
		name:		收藏人的名字
		avatar:		收藏人的头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户 
	4) 正文url
	piclist:		多个图片组合起来的数组
	pic:			图片地址	
	title：			图片标题
	message:		该组照片的描述,正文  =  piclist + message 组合起来显示
	5）
	lng：			经度
	lat：			纬度
	address：		地点名称
	6） 和谁在一起
	together：		多维数组
		uid:		在一起的人的uid
		name:		在一起的人的名字
		avatar:		在一起的人的头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
	7) 评论（表态）
	commentlist:多维数组
		authorid：	评论人uid
		avatar:		评论人头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
		message：	评论内容
	8) 发布渠道 
	come:			发布渠道
 
<h3>1．5、	</h3><h3>日记详情接口</h3>
【参数】  
>  
	
	do:	 		blog
	uid:  		日志发布人的uid  
	id:	 		日志id 
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】
网站域名/dapi/space.php?do=blog&id=18&uid=?&m_auth=?   
【返回值】  
>  
		
	1）
	uid:			发布者的uid
	name:			发布者的name  
	avatar:			发布者的头像  
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	note:			关系备注
	dateline:		发布时间
	subject:		标题
	tag:
		tagid:		空间id
		tagname:	空间名称
	2）转采
	fuid:			转采uid
	fname:			转采者名字
	3） 
	reblognum：		转采数量
	replynum：		评论数量
	love:			收藏数量
	loveuser：		收藏人列表【多维数组】
		uid:		在一起的人的uid
		name:		在一起的人的名字
		avatar:		在一起的人的头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户 
	4) 正文url
	message:		正文的内容， html格式的
	5）
	lng：			经度
	lat：			纬度
	address：		地点名称
	6） 和谁在一起
	together：		多维数组
		uid:		收藏人的uid
		name:		收藏人的名字
		avatar:		收藏人的头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
	7) 评论（表态）
	commentlist:多维数组
		authorid：	评论人uid
		avatar:		评论人头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
		message：	评论内容
	8) 发布渠道 
	come:			发布渠道

 
<h3>1．6、	</h3><h3>视频详情接口</h3>
【参数】  
>  
	
	do:	 		video
	uid: 		视频发布人的uid  
	id:	 		视频id  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=video&id=4&uid=?&m_auth=?    
【返回值】  
>  
		
	1）
	uid:			发布者的uid
	name:			发布者的name  
	avatar:			发布者的头像  
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	note:			关系备注
	dateline:		发布时间
	subject:		标题
	tag:
		tagid:		空间id
		tagname:	空间名称
	2）转采
	fuid:			转采uid
	fname:			转采者名字
	3） 
	revideonum：	转采数量
	replynum：		评论数量
	love:			收藏数量
	loveuser：		收藏人列表【多维数组】
		uid:		收藏人的uid
		name:		收藏人的名字
		avatar:		收藏人的头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户 
	4) 视频url
	videourl:		视频url
	subject:		视频标题
	5）
	lng：			经度
	lat：			纬度
	address：		地点名称
	6） 和谁在一起
	together：		多维数组
		uid:		在一起的人的uid
		name:		在一起的人的名字
		avatar:		在一起的人的头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
	7) 评论（表态）
	commentlist:多维数组
		authorid：	评论人uid
		avatar:		评论人头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
		message：	评论内容
	8) 发布渠道 
	come:			发布渠道

 
<h3>1．7、	</h3><h3>活动详情接口</h3>  
【参数】  
>  

	do:	 		event
	uid:  		活动发布人的uid  
	id:	 		活动id
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=event&id=223&uid=?&m_auth=?  
【返回值】  
>  

	1）
	uid:			发布者的uid
	name:			发布者的name  
	avatar:			发布者的头像  
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	note:			关系备注
	dateline:		发布时间
	title:			标题
	tag:
		tagid:		空间id
		tagname:	空间名称
	2）转采
	fuid:			转采uid
	fname:			转采者名字
	3） 
	reeventnum：	转采数量
	replynum：		评论数量
	love:			收藏数量
	loveuser：		收藏人列表【多维数组】
		uid:		收藏人的uid
		name:		收藏人的名字
		avatar:		收藏人的头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户 
	4) 活动信息
	title:			活动标题
	detail：		活动主要内容, html形式
	dateline:		活动时间
	lng：			经度
	lat：			纬度
	location：		活动地点
	5） 和谁在一起
	together：		多维数组
		uid:		在一起的人的uid
		name:		在一起的人的名字
		avatar:		在一起的人的头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
	6) 评论（表态）
	commentlist:多维数组
		authorid：	评论人uid
		avatar:		评论人头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
		message：	评论内容
	7) 发布渠道 
	come:			发布渠道
	7) 活动成员 
	members【数组】:  
		uid:		参加者的uid
		name:		参加者的名字
		dateline:	参加时间
	
	

 
<h3>1．8、	</h3><h3>评论列表接口</h3>  
【参数】  
>  

	do:			comment
	id:			被评论的对象id
	idtype:		被评论的类型(photoid: 照片,  'eventid': 活动,  'blogid'：日志,  'videoid'：视频)
	page:		当前页，默认1
	perpage:	每页数量，默认10
	starttime:	取数据的开始时间，不包含变量自身, 默认空值不设置数据范围 
	endtime:	取数据的结束时间，不包含变量自身, 默认空值不设置数据范围 
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=comment&id=293&idtype=photoid  
【返回值】  
>  

	authorid:		评论用户uid
	avatar:			头像url
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	authorname:		评论用户名
	note:			关系备注
	message:		评论内容
	dateline:		评论时间
	lng:			经度
	lat:			纬度
	address:		地名
	come:			发布来源
	candel:			是否有删除权限，1：有 0：无

<h3>1．9、	</h3><h3>个人空间接口</h3>  
【参数】  
>  
	
	uid:  		自己的uid, 无则代表登陆用户的uid  
	page:		空间的当前页，默认1
	perpage:	空间的分页数, 默认4
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?m_auth=?
【返回值】  
>  

	1）
	uid:			用户id
	name:			用户名字
	avatar:			用户头像url
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	feeds:			动态数量
	fmembers:		家人数量	
	birthday：		生日
	2）家人列表
	fmemberlist：	家人列表数组
		uid:		家人uid
		name:		家人名字
		avatar:		家人头像
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
		note：		关系备注
		birthday：	生日
	3) 空间列表
	spacelist:		数组
		tagid:		空间id
		tagname:	空间名称		
		blogs:		空间日志数
		photos:		空间照片数
		events:		空间活动数
		videos:		空间视频数
		pic:		空间最新一张图片

 
<h3>1．10、	</h3><h3>空间内容列表接口</h3>  
【参数】  
>  

	uid:			用户id, 无则代表登陆用户的uid  
	tagid:			空间id
	page:			当前页，默认1
	perpage:		每页大小，默认1 (如果是ipad版本，可以传递大点的值过来,比如：10)  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=familyspace&m_auth=?&tagid=?  
【返回值】  
>  

	tagname:		标签名，即：网站详情中的概述
	feednum:		该标签的信息数量
	feedlist:		信息详情，【数组】
		image_1		图片地址
		imagesize	图片信息
			height: 图片高度
			width:	图片宽度
		idtype:		信息的类型，包括（'blogid','photoid','eventid','videoid','reblogid','rephotoid','reeventid','revideoid'）
		id:			信息的id
		uid:		该条信息的发布人uid
		name:		该条信息的发布人昵称
		subject:	标题
		message:	概述
		commentlist 评论内容【数组】
			authorid	评论人的uid
			author		评论人的用户名
			authorname	评论人的昵称
			message		评论内容

 
<h3>1．11、	</h3><h3>对话列表接口</h3>  
【参数】  
>  

	uid:		用户id, 无则代表登陆用户的uid  
	page:		当前页, 默认1
	perpage:	分页大小，默认10
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=pm&filter=privatepm&m_auth=?   
【返回值】  
>  

	data:		数组
		touid:					对话对方用户uid
		msgtoname:				对话对方name
		msgtoavatar:			对方对方的头像url
		note:					备注名
		lastdateline:			最后对话的时间
		lastsummary:			最后对话的内容
		lng:					最后对话纬度
		lat:					最后对话经度
		address;				最后对话地点
		come:					最后对话发布来源
		new:					这个对话中是否有未读消息 1是， 0否
		newnum:					这个对话中有几个未读消息的数量
 
<h3>1．12、	</h3><h3>对话详情接口</h3>  
【参数】  
>  

	uid:		用户id, 无则代表登陆用户的uid  
	touid: 		对话的用户id
	page:		当前页, 默认1
	perpage:	分页大小，默认10  
	daterange	时间范围(1:最近一天，2：最近两天 3:最近三天 4:本周 5:全部)，默认为5 
	starttime:	取数据的开始时间，不包含变量自身, 默认空值不设置数据范围, 设置了此变量后，daterange参数将失效 
	endtime:	取数据的结束时间，不包含变量自身, 默认空值不设置数据范围 
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=pm&subop=view&m_auth=?&touid=4  
【返回值】  
>  

	fromuser: 	
		uid:			当前用户的uid
		name:			当前用户的name
		avatar:			头像url
		vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
		lastmsgtime:	最后一条对话的时间
	touser: 	
		uid:			对方的uid
		name:			对方的name
		avatar:			对方头像url
		vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	dialog: 多条信息的数组
		msgfromid:		发信人uid
		msgtoid:		接收信息人uid
		message:		信息内容
		dateline:		发信时间
		lng:			经度
		lat:			纬度
		address:		地名
		come:			发布来源


<h3>1．13、	</h3><h3>通知列表接口</h3>  
【参数】  
>  

	uid:			用户id, 无则代表登陆用户的uid  
	page:			当前页, 默认1
	perpage:		分页大小，默认10 
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=notice&m_auth=?  
【返回值】  
>  

	1）	
	authorid:			发通知的用户uid
	authouravatar:		头像url
	vipstatus:			personal: 个人, family： 家庭， 空值：普通用户
	authourname:		发通知的用户昵称
	note:				通知详情(仅仅供参考, 不用来显示)
	notesplit:			拆分后的通知内容   
		action：		通知主语   
		obj：   		操作的对象   
			uid			发布该对象的用户id   
			id			该对象的id   
			idtype		该对象的类型  
			subject		该对象的标题  
		withfriends 	和谁在一起【数组】 
			uid			在一起的用户id  
			name		在一起的人的名字  
	address:			在什么地方
	通过以上字段，就可以组合成一句完整的通知语句  
	2）	通知详情内如果包含其他用户的话
	fuid:				其他用户uid
	fname:				name
	3）	通知详情内如果包含某个帖子
	fid:				其它帖子的id
	ftitle:				其他帖子的标题
	4）	通知的阅读状况
	new:				0已读, 1未读
 
<h3>1．14、	</h3><h3>更多信息接口</h3>  
【参数】  
>  

	uid:			用户id, 无则代表登陆用户的uid  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=setup&m_auth=?  
【返回值】  
>  

	uid:			用户id
	name:			用户名字
	avatar:			用户头像url
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	phone:			电话号码
	birthday：		生日
	fmembers:		家人数量
	frequests:		家人申请数量
	credit:			金币
	tasknum:		有奖任务
	lovenum:		收藏数量
	babylist:【数组】孩子
		babyid		 孩子id
		uid			 孩子所属的uid
		babyname	 孩子名称
		babysex		 孩子性别
		babybirthday 孩子生日
		babyavatar	 孩子头像
		tagid		 孩子所属的空间详情的id
	
	存客户端:		主题
	sina_uid:		是否绑定新浪微博，有uid则说明绑定
	is_qq_bing:		是否绑定qq
	ispush			是否推送，1是
 
<h3>1．15、	</h3><h3>用户名片接口</h3>  
【参数】  
>  

	uid:			自己的用户id, 无则代表登陆用户的uid  
	fuid:			对方的用户id  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=friend&m_auth=?&fuid=?  
【返回值】  
>  

	uid:			对方的uid
	name:			对方的昵称
	phone:			对方的电话号码
	avatar:			对方的头像
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	isfamily:		是否是我的家人，1：是，0：否
	birthday:		对方生日
	fmembers：		对方的家人数量
	tags:			空间数量
	note：			关系备注
	lastlogin:		最后一次登录时间

 
<h3>1．16、	</h3><h3>家人列表接口</h3>  
【参数】  
>  

	uid:		用户id, 无则代表登陆用户的uid    
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=fmembers&m_auth=?  
【返回值】  
>  

	uid:				自己的用户id
	name:				自己的昵称
	avatar:				自己的头像
	vipstatus:			personal: 个人, family： 家庭， 空值：普通用户
	fmembers：			自己的家人数量
	frequests:			自己的家人申请数量
	fmemberlist：家人列表【数组】
			uid			家人的用户id
			username	家人的电话号码
		    name		家人的昵称
		    avatar：	家人的头像
		    note:		家人关系备注 
		    feeds:		家人动态数量 
		    fmembers：	家人的家人数量
		    birthday：	家人的生日
			


<h3>1．17、	</h3><h3>搜索家人接口</h3>  
【参数】  
>  

	uid:				用户id, 无则代表登陆用户的uid   
	page:				当前页，默认为1 
	perpage:			每页数量，默认为10 
	fsearch:			提交搜索的标志，固定值1 
	kw:					搜索的关键词,可以是电话号码或者名称  
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/ space.php?do=fmembers&m_auth=?&fsearch=1&kw=小宝  
【返回值】  
>  

	uid:			自己的用户id
	name:			自己的昵称
	avatar:			自己的头像
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	fmembers：		自己的家人数量
	fmemberlist：家人列表【数组】
		uid			家人的用户id
	    name		家人的昵称
	    avatar：	家人的头像
	    note:		家人关系备注 
	    feeds:		家人动态数量 
	    fmembers：	家人的家人数量  
		birthday：	家人的生日  
		isfamily:	是否已经成为家人，1已经是家人，0不是  

 
<h3>1．18、	</h3><h3>家人申请接口</h3>  
【参数】  
>  
	
	uid:			用户id, 无则代表登陆用户的uid    
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=request&m_auth=?    
【返回值】  
>  
	
	uid:				自己的用户id
	name:				自己的昵称
	avatar:				自己的头像
	vipstatus:			personal: 个人, family： 家庭， 空值：普通用户
	fmembers：			自己的家人数量
	requestnum:			家人申请数量
	requestlist:申请人列表【数组】
		uid:			用户id
		phone:			电话号码
		name:			用户昵称
		avatar:			用户头像
		vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
		dateline:		申请时间

 
<h3>1．19、	</h3><h3>有奖任务列表接口</h3>  
【参数】  
>  

	do:			task
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=task&m_auth=?  
【返回值】  
>  
	
	uid:			自己的用户id
	name:			自己的昵称
	avatar:			自己的头像
	vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
	tasknum:		未完成的有奖任务数
	tasklist:【数组】有奖任务列表
		taskid：	任务id
		image：		任务图标
		name：		任务名称
		note:		任务简介
		credit：	奖励金币数量


<h3>1．20、	</h3><h3>随机有奖任务提醒</h3>  
【参数】  
>  
	
	do:			task 
	op:			rand 
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=task&op=rand  
【返回值】  
>  
	
	taskid：	任务id
	image：		任务图标
	name：		任务名称
	note:		任务简介

 
<h3>1．21、	</h3><h3>有奖任务详情</h3>  
【参数】  
>  
	
	do:			task 
	taskid:		某个任务的id  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/space.php?do=task&taskid=1  
【返回值】  
>  
	
	taskid：	任务id
	image：		任务图标
	name：		任务名称
	note:		任务简介
	xyz:		是否已经满足条件、未满足条件下前往的页面（x.y.z）
	
<h3>1．22、	</h3><h3>微信家庭动态列表接口</h3>  
【参数】  
>  
	
	do:	 		wxfeed
	perpage: 	分页大小， 默认5
	page:		当前页
	wxkey:		用户微信key

	
【调用方式】  
网站域名/dapi/space.php?do=wxfeed  
【返回值】  
>  
	
	data【多维数组】 
		uid				用户id
		username		用户昵称
		avatar: 		发布用户头像url
		vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
		id: 			被操作的对象id
		idtype: 		动态类型(
							eventid: 		发布活动
							reeventid：		转采活动
							blogid: 	 	发布日志
							reblogid： 		转采日志
							photoid：	  	上传图片
							rephotoid：		转采图片
							videoid：		发布视频
							revideoid：		转采视频
						)
		title: 			动态标题
		image_1 		动态带的图片
		message:		动态简介文字  
		
	如果wxkey不对，则服务器会返回:  
	data
		return:		-1
	
<h3>1．23、	</h3><h3>m_auth验证接口</h3>  
【参数】  
>  
	
	ac:	 		ckmauth
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

	
【调用方式】  
网站域名/dapi/do.php?ac=ckmauth&m_auth=?
【返回值】  
>  
	
	data
		return: 1：验证通过  2：验证失败 (需要重新登录得到新的m_auth)
 
<h3>1．24、	</h3><h3>pm版本统计接口</h3>  
【参数】  
>  

	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=elder&m_auth=?  
【返回值】  
>  

	addphoto:		新图片数量  
	addblog:		新日志数量  
	addevent:		新活动数量  
	addvideo:		新视频数量  
	pmcount：		新对话数量  
	applycount：	家人申请数量  
	notecount：		新通知总数  

<h3>1．25、	</h3><h3>pm版本动态接口</h3>  
【参数】  
>  

	do:	 		pmfeed
	uid:		用户id, 无则代表登陆用户的uid  
	perpage: 	分页大小， 默认10
	page:		当前页
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	idtype:		动态的类型【可选】，默认为空（代表全部），如果指定值（则只得到该类型的动态）
【调用方式】  
网站域名/dapi/space.php?do=pmfeed&m_auth=?    
【返回值】  

>

	1）多维数组：  
		uid:			行为人uid
		id：			被操作对象的id
		idtype:			被操作的对象类型

		
<h3>1．26、	</h3><h3>空间详情简化接口</h3>  
【参数】  
>  

	uid:			用户id, 无则代表登陆用户的uid  
	tagid:			空间id
	page:			当前页，默认1
	perpage:		每页大小，默认1 (如果是ipad版本，可以传递大点的值过来,比如：10)  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/space.php?do=familyspacesimple&m_auth=?&tagid=?  
【返回值】  
>  

	tagname:		空间名，即：网站详情中的概述
	feednum:		该标签的信息数量
	feedlist:		信息详情，【数组】
		idtype:		信息的类型，包括（'blogid','photoid','eventid','videoid','reblogid','rephotoid','reeventid','revideoid'）
		id:			信息的id
		uid:		该条信息的发布人uid
		dateline:	时间

<h3>1．27、	</h3><h3>我收藏的帖子的动态列表接口</h3>  
【参数】  
>  

	do:	 		lovefeed
	uid:		用户id, 无则代表登陆用户的uid  
	perpage: 	分页大小， 默认10
	page:		当前页
	date:		指定某天的动态【格式:2013-08-21】，默认空，为空时则取全部动态
	dayfeed:	默认为空值，设为：1 则动态按天分组
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	idtype:		动态的类型【可选】，默认为空（代表全部），如果指定值（则只得到该类型的动态）
【调用方式】  
网站域名/dapi/space.php?do=lovefeed&m_auth=?    
【返回值】  

>

	1）多维数组：  
		avatar: 		发布用户头像url
		vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
		name: 			用户昵称
		note : 			关系备注
		dateline: 		动态时间
		tag:
			tagid:		空间id
			tagname:	空间名称
		idtype: 		动态类型(
				eventid: 		发布活动
				reeventid：		转采活动
				eventcomment：	活动评论
				blogid: 	 	发布更新日志
				reblogid： 		转采日志
				blogcomment： 	日志评论
				photoid：	  	上传图片
				photocomment： 	评论图片
				rephotoid：		转采图片
				videoid：		发布视频
				revideoid：		转采视频
				videocomment：	视频评论
				profield: 		更新资料
				avatar:  		更新头像
		)
		replynum		评论数量
		reblognum		转发数量
		love			收藏数量
		picnum			照片数量
		mylove			是否是我收藏的，1：是，0：否
		eventdetail		活动详情   
        eventstarttime	活动时间  
	2）转采  
		fuid				原作者uid
		fname				原作者名称
	3)普通动态  
		title: 				动态标题
		image_1 – image_4:	动态带的图片和内容附图的数量, 如果有图片则有值，否则为空值
		message:			动态简介文字
		id:					原文id
		fuid:				原文所属于的空间id
		fname:				原文所属于的空间名称
		fmessage:			原文内容
	4） 活动动态  
		lng:				活动地点的经度
		lat:				活动地点的纬度
		location:			活动地点的地名
	5） 行为动态  
		uid:				行为人uid
		name:				行为人名字
		fuid:				对象人uid
		fname:				对象人名字
		subject：			被操作的对象名称
		id：				被操作的id
		idtype：			被操作的类型
	6) 发布渠道 
		come: 				发布的渠道  
	
	7） 最新的两条评论  
		comment： 	数组
			authorid：		评论人的uid
			authorname:		评论人的名字
			message：		评论内容
			dateline：		评论时间

		loveuser 收藏人列表(数组)
			uid				收藏人uid
			name			收藏人名字
			avatar			收藏人头像
			vipstatus		收藏人身份(personal: 个人, family： 家庭， 空值：普通用户)  
			
			
<h3>1．28、	</h3><h3>pm版本收藏动态接口</h3>  
【参数】  
>  

	do:	 		pmfeed
	uid:		用户id, 无则代表登陆用户的uid  
	perpage: 	分页大小， 默认10
	page:		当前页
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	idtype:		动态的类型【可选】，默认为空（代表全部），如果指定值（则只得到该类型的动态）
【调用方式】  
网站域名/dapi/space.php?do=lovefeedpm&m_auth=?    
【返回值】  

>

	1）多维数组：  
		uid:			行为人uid
		id：			被操作对象的id
		idtype:			被操作的对象类型 
	

<h3>1．29、	</h3><h3>高德地图POI接口</h3>  
【参数】  
>  

	lng:	 	经度，6位小数，如：
	lat:		维度，6位小数, 如：
	range:		范围，默认3000, 单位米  
	perpage: 	分页大小， 默认10
	page:		当前页, 默认1
	keyword:    关键词，如：酒店
【调用方式】  
网站域名/dapi/map.php?lng=?&lat=?  
【返回值】  

>

	1）多维数组：  
		name:			名称
		address			地址
		tel:			电话
		type:			类型
		lng:			经度
		lat:			纬度
		

<h3>1．30、	</h3><h3>客户端升级接口</h3>  
【参数】  
>  

	type:	 	客户端类型(可选值：iphone,ipad,android,winphone,iphonepm,androidpm,cube)
【调用方式】  
网站域名/dapi/upgrade.php?type=?  
【返回值】  

>

	data：  
		version:		版本号
		versionname:	版本名称
		upgradeinfo		升级信息
		upgradedate:	升级日期
		
<h3>1.31、	</h3><h3>上传用户查询用户接口</h3>  
【参数】  
>  
	
	unames:	 上传上去的用户，手机号和名称中间用":"连接，多个用"|"连接，如：13578909878:弟弟| 13578909879:妹妹
	m_auth:	 API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】【POST方式】 
网站域名/dapi/dapi/cp.php?ac=friend&op=find  
【返回值】  
>  
	data【多维数组】
		uid:		用户uid，如果没找到，则返回字符串
		username:	上传时的手机号
		name:		上传时的名字
		avatar:		头像, 如果没找到用户，则返回空字符串
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错 

	
<h3>1.32、</h3><h3>新的动态数量接口</h3>  
【参数】   
>   

	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	
【调用方式】  
网站域名/dapi/space.php?do=feednew&m_auth=?   
【返回值】  
>  
	data
		newfeednum			新的动态的数量		

 
<h3>1．33、	</h3><h3>家庭动态列表按天分组接口</h3>  
【参数】  
>  

	do:	 		feedday
	uid:		用户id, 无则代表登陆用户的uid  
	perpage: 	分页大小， 默认10
	page:		当前页
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	idtype:		动态的类型【可选】，默认为空（代表全部），如果指定值（则只得到该类型的动态）
	apptype:	默认为空[显示全部类型的动态], 设为pm[则去掉评论以及行为动态]
	date:		指定日期的动态，格式: 2013-08-01
【调用方式】  
网站域名/dapi/space.php?do=feedday&m_auth=?    
【返回值】  

>
	
	dateline【每天的时间戳】  

		1）多维数组：  
			avatar: 		发布用户头像url
			vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
			name: 			用户昵称
			note : 			关系备注
			dateline: 		动态时间
			tag:
				tagid:		空间id
				tagname:	空间名称
			idtype: 		动态类型(
					eventid: 		发布活动
					reeventid：		转采活动
					eventcomment：	活动评论
					blogid: 	 	发布更新日志
					reblogid： 		转采日志
					blogcomment： 	日志评论
					photoid：	  	上传图片
					photocomment： 	评论图片
					rephotoid：		转采图片
					videoid：		发布视频
					revideoid：		转采视频
					videocomment：	视频评论
					profield: 		更新资料
					avatar:  		更新头像
			)
			replynum		评论数量
			reblognum		转发数量
			love			收藏数量
			picnum			照片数量
			mylove			是否是我收藏的，1：是，0：否
			eventdetail		活动详情   
			eventstarttime	活动时间  
		2）转采  
			fuid				原作者uid
			fname				原作者名称
		3)普通动态  
			title: 				动态标题
			image_1 – image_4:	动态带的图片和内容附图的数量, 如果有图片则有值，否则为空值
			image_1_width – image_4_width:		动态图片的宽度
			image_1_height – image_4_height:	动态图片的高度
			message:			动态简介文字
			id:					原文id
			fuid:				原文所属于的空间id
			fname:				原文所属于的空间名称
			fmessage:			原文内容
		4） 活动动态  
			lng:				活动地点的经度
			lat:				活动地点的纬度
			location:			活动地点的地名
		5） 行为动态
			
			普通的行为动态：
			uid:				行为人uid
			name:				行为人名字
			fuid:				对象人uid
			fname:				对象人名字
			
			评论的行为动态(即：idtype为：**comment的)：
			cuid:				评论人uid
			cname:				评论人名字
			cavatar: 			评论人头像
			cvipstatus:			personal: 个人, family： 家庭， 空值：普通用户
			uid:				被评论对象人uid
			name:				被评论对象人名字
			
			------------------------------
			subject：			被操作的对象名称
			id：				被操作的id
			idtype：			被操作的类型
			
		6) 发布渠道 
			come: 				发布的渠道  
		
		7） 最新的两条评论  
			comment： 	数组
				authorid：		评论人的uid
				authorname:		评论人的名字
				message：		评论内容
				dateline：		评论时间
			
			loveuser 收藏人列表(数组)
				uid				收藏人uid
				name			收藏人名字
				avatar			收藏人头像
				vipstatus		收藏人身份(personal: 个人, family： 家庭， 空值：普通用户)  

				
<h3>1．34、	</h3><h3>家庭行为动态列表接口</h3>  
【参数】  
>  

	do:	 		feedact
	uid:		用户id, 无则代表登陆用户的uid  
	perpage: 	分页大小， 默认10
	page:		当前页
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	idtype:		动态的类型【可选】，默认为空（代表全部），如果指定值（则只得到该类型的动态）
【调用方式】  
网站域名/dapi/space.php?do=feedday&m_auth=?    
【返回值】  

>

	1）多维数组：  
		avatar: 		发布用户头像url
		vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
		name: 			用户昵称
		note : 			关系备注
		dateline: 		动态时间
		tag:
			tagid:		空间id
			tagname:	空间名称
		idtype: 		动态类型(
				eventid: 		发布活动
				reeventid：		转采活动
				eventcomment：	活动评论
				blogid: 	 	发布更新日志
				reblogid： 		转采日志
				blogcomment： 	日志评论
				photoid：	  	上传图片
				photocomment： 	评论图片
				rephotoid：		转采图片
				videoid：		发布视频
				revideoid：		转采视频
				videocomment：	视频评论
				profield: 		更新资料
				avatar:  		更新头像
		)
		replynum		评论数量
		reblognum		转发数量
		love			收藏数量
		picnum			照片数量
		mylove			是否是我收藏的，1：是，0：否
		eventdetail		活动详情   
		eventstarttime	活动时间  
	2）转采  
		fuid				原作者uid
		fname				原作者名称
	3)普通动态  
		title: 				动态标题
		image_1 – image_4:	动态带的图片和内容附图的数量, 如果有图片则有值，否则为空值
		image_1_width – image_4_width:		动态图片的宽度
		image_1_height – image_4_height:	动态图片的高度
		message:			动态简介文字
		id:					原文id
		fuid:				原文所属于的空间id
		fname:				原文所属于的空间名称
		fmessage:			原文内容
	4） 活动动态  
		lng:				活动地点的经度
		lat:				活动地点的纬度
		location:			活动地点的地名
	5） 行为动态
		
		普通的行为动态：
		uid:				行为人uid
		name:				行为人名字
		fuid:				对象人uid
		fname:				对象人名字
		
		评论的行为动态(即：idtype为：**comment的)：
		cuid:				评论人uid
		cname:				评论人名字
		cavatar: 			评论人头像
		cvipstatus:			personal: 个人, family： 家庭， 空值：普通用户
		uid:				被评论对象人uid
		name:				被评论对象人名字
		
		------------------------------
		subject：			被操作的对象名称
		id：				被操作的id
		idtype：			被操作的类型
		
	6) 发布渠道 
		come: 				发布的渠道  
	
	7） 最新的两条评论  
		comment： 	数组
			authorid：		评论人的uid
			authorname:		评论人的名字
			message：		评论内容
			dateline：		评论时间
		
		loveuser 收藏人列表(数组)
			uid				收藏人uid
			name			收藏人名字
			avatar			收藏人头像
			vipstatus		收藏人身份(personal: 个人, family： 家庭， 空值：普通用户)  

 						
<h3>1.35、</h3><h3>每日图片接口</h3>  
【参数】  
无  
【调用方式】  
网站域名/dapi/info.php?ac=adpic  
【返回值】  
> 

	picurl	图片url  

  		
	
<h2>第二部分 </h2><h2>上行接口部分</h2>
==================


<h3>2.1、	</h3><h3>普通登录接口</h3>  
【参数】  
>  

	username:		账号
	password:		密码
	iscookie:		是否保存密码，为1时保存 
	
	如果需要绑定新浪微博，需要提供以下参数【可选】： 
	sina_uid			新浪微博用户id
	sina_token			新浪微博token
	sina_expires_in		新浪微博token过期时间(格式：2013-05-12 22:59:59)
	
	如果需要绑定腾讯微博，需要提供以下参数【可选】： 
	qq_openid		腾讯微博用户id
	qq_token		腾讯微博token
	
【调用方式】  
网站域名/dapi/do.php?ac=login  
【返回值】  
>  
	
	data:
	 return: 返回的状态码，
			-1： 用户名或者密码为空
			-2： 用户名或者密码错误
			 1： 登录成功
	 m_auth:   登录成功后返回的登录密匙，请求每个接口都需要发送这个参数给服务器,重新登录时，这个值会改变。
	 uid:	   用户的uid  
	 username: 用户名  
	 name:     用户昵称  
	 avatar:   用户头像  
	 vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
	 credit：  本次登录的积分
	 experience 本次登录的经验
	 is_sina_bind 是否绑定新浪微博 1 是 0 否
	 is_qq_bind   是否绑定腾讯微博 1 是 0 否
	 
<h3>2.2、	</h3><h3>第三方登录接口</h3>  
【参数】  
>  
	
	token:			[这个参数已经没用了,可传可不传]
	
	logintype:		weibo: 新浪微博, qq：腾讯微博  
	新浪微博登录
	sina_uid		微博的uid 
	腾讯微博登陆
	qq_openid		腾讯微博的id  
	
	参数的组合方式：(weibo + sina_uid) 或者 (qq + qq_openid)  
	
【调用方式】  
网站域名/dapi/do.php?ac=login  
【返回值】  
>  
	
	data:
		return:	返回的状态码
			-1：token的uid参数为空
			-2：token的uid未绑定
			 1：登录成功
		m_auth: 登录成功后返回的登录密匙，请求每个接口都需要发送这个参数给服务器,重新登录时，这个值会改变  
		uid:	   用户的uid  
		username: 用户名  
		name:     用户昵称  
		avatar:   用户头像  
		vipstatus:	personal: 个人, family： 家庭， 空值：普通用户
		credit：  本次登录的积分
		experience 本次登录的经验
		is_sina_bind 是否绑定新浪微博 1 是 0 否  
		is_qq_bind   是否绑定腾讯微博 1 是 0 否  

 
<h3>2.3、	</h3><h3>注册接口</h3>  
【参数】  
>  
	注册前调用 2.43、注册获取验证码接口
	
	username:		注册用户名(手机号)
	name:			用户昵称
	password:		密码
	seccode:		手机验证码  
	
	如果需要绑定新浪微博，需要提供以下参数【可选】： 
	sina_uid			新浪微博用户id
	sina_token			新浪微博token
	sina_expires_in		新浪微博token过期时间(格式：2013-05-12 22:59:59)
	
	如果需要绑定腾讯微博，需要提供以下参数【可选】： 
	qq_openid		腾讯微博用户id
	qq_token		腾讯微博token
【调用方式】  
网站域名/dapi/do.php?ac=register  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错
	data:
					return:	返回的状态码
						-1：用户名或者密码为空
						-2：用户名或者密码错误
						 1：登录成功
					m_auth: 注册成功后返回的登录密匙，需要保持在客户端。
					uid:	   用户的uid  
					username:  用户名  
					name:      用户昵称  
					avatar:    用户头像  
					vipstatus:   personal: 个人, family： 家庭， 空值：普通用户
					is_sina_bind 是否绑定新浪微博 1 是 0 否  
					is_qq_bind   是否绑定腾讯微博 1 是 0 否  

 
<h3>2.4、	</h3><h3>个人头像和昵称设置接口</h3>  
【参数】  
修改头像：  
>  
	
	Filedata:		文件上传变量
	avatarsubmit：	提交表单用的验证，设为1即可  
	m_auth:		    API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
修改昵称：  
>  

	name:			昵称
	namesubmit：	提交表单用的验证，设为1即可
	m_auth:		    API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
修改头像：网站域名/dapi/cp.php?ac=avatar  
修改昵称：网站域名/dapi/cp.php?ac=name  
【返回值】  
>  
	
	data:
		reward:
			credit:			返回的积分
			experience：	返回的经验


 
<h3>2.5、	</h3><h3>添加孩子接口</h3>  
【参数】  
>  
	
	babyname:			孩子姓名
	babysex:			孩子性别
	babybirthday:		孩子出生年月
	pic:				孩子头像url，调用2.21单张图片上传接口得到pic
	babysubmit：		提交表单用的验证，设为1即可  
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=baby  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错



 
<h3>2.6、	</h3><h3>创建空间接口</h3>  
【参数】  
>
	
	tagname:		空间名
	pic:			空间封面照片(url), 可以通过利用上传单张图片接口上传
	tagsubmit：		提交表单用的验证，设为1即可  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=tag  
【返回值】  
>

	data
        tagid:		   空间id  
        tagname:       空间名称  
        default_image: 空间默认的图片  
 
<h3>2.7、	</h3><h3>申请成为家人接口</h3>  
【参数】  
>  
	
	uid:			自己的uid, 无则代表登陆用户的uid  
	applyuid:		对方的uid
	gid:			申请的分组
	note:			申请时的附带信息
	addsubmit：		提交申请表单用的验证，设为1即可  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/dapi/cp.php?ac=friend&op=add  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错 
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  


<h3>2.8、	</h3><h3>同意成为家人接口</h3>  
【参数】  
>  
	
	applyuid:		申请人的uid
	gid:			分组id
	notename:		对方家人的备注
	agreesubmit：	同意申请，设为1即可  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=add  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错

<h3>2.9、	</h3><h3>收藏动态</h3>  
【参数】  
>  
	
	id				被收藏的对象id
	idtype			被收藏的对象id类型(如：blogid, videoed)
	type			是增加还是取消收藏，1添加到收藏，0取消收藏  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=feedlove  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错

<h3>2.10、	</h3><h3>评论接口</h3>  
【参数】  
>  
	
	id				被评论的对象id
	idtype			被评论的对象id类型(blogid, videoid, photoid, eventid)，转发的也是这几个
	message			评论内容  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=comment  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错

 
<h3>2.11、	</h3><h3>参加活动接口</h3>  
【参数】  
>  
	
	id				活动id
	idtype			eventid
	message			我要参加活动!
	come			发布来源（iphone或者ipad，客户端生成）  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=comment  
【返回值】  
>  
	
	data	【数组】
		selfreward		参加者的奖励【数组】
		credit			金币
		experience		经验
		toreward		活动发起人的奖励【数组】
		credit			金币
		experience		积分


<h3>2.12、	</h3><h3>表态接口</h3>  
【参数】  
>  
	
	id			被表态对象的id
	idtype		被表态对象的类型(eventid,blogid,vedioid,photoid)
	clickid		表态类型的id，一个id可以对应一个表态的类型，如：鲜花，雷人
	come		发布来源（iphone或者ipad，客户端生成）  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=click&op=add  
【返回值】  
>  
	
	data	【数组】
		reward			表态者的奖励【数组】
		credit			金币
		experience		经验

 
<h3>2.13、	</h3><h3>发消息对话接口</h3>  
【参数】  
>  
	
	touid		对方的uid
	pmid		对话列表的id
	message		消息内容
	lat			纬度（客户端生成）
	lng			经度（客户端生成）
	address		发布地址（客户端生成）
	come		发布来源（iphone或者ipad或者android，客户端生成）
	pmsubmit	提交信息的表单验证，设为1即可  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=pm&op=send  
【返回值】  
>  
	
	msgkey：			信息提示码
	msg：				返回的提示信息
	error:				返回的错误的状态, 0无错误，1出错

<h3>2.14、	</h3><h3>修改头像接口</h3>  
【参数】  
修改头像：  
>  
	
	Filedata:			文件上传变量
	avatarsubmit：		提交表单用的验证，设为1即可  
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
修改头像：网站域名/dapi/cp.php?ac=avatar  
【返回值】  
>  
	
	data:
		reward:
			credit:		返回的积分
			experience：返回的经验

<h3>2.15、	</h3><h3>修改昵称接口</h3>  
【参数】  
>  
	
	name:				昵称
	namesubmit：		提交表单用的验证，设为1即可  
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=name  
【返回值】  
>  
	
	data:
		reward:
			credit:		返回的积分
			experience：返回的经验
 
<h3>2.16、	</h3><h3>修改生日接口</h3>  
【参数】  
>  
	
	birth:				生日,格式(1989-08-12)
	birthsubmit：		提交表单用的验证，设为1即可  
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=birth  
【返回值】  
>  
	
	msgkey：			信息提示码
	msg：				返回的提示信息
	error:				返回的错误的状态, 0无错误，1出错

 
<h3>2.17、	</h3><h3>参加有奖任务接口</h3>  
【参数】  
>  
	
	taskid		任务的id  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=task&op=do  
【返回值】  
>  
	
	data:  
		credit:			返回奖励的积分
		spacecredit：	返回领奖后总的积分


<h3>2.18、	</h3><h3>修改备注关系接口</h3>  
【参数】  
>  
	
	fuid					被备注人的uid
	note					关系备注名称
	changenotesubmit		1  
	m_auth:					API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=changenote  
【返回值】  
>  
	
	msgkey：				信息提示码
	msg：					返回的提示信息
	error:					返回的错误的状态, 0无错误，1出错

<h3>2.19、	</h3><h3>修改生日提醒接口</h3>  
【参数】  
>  
	
	fuid					被设置生日的人的uid
	notebirth				生日日期
	changenotesubmit		1  
	m_auth:					API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=changenote  
【返回值】  
>  
	
	msgkey：			信息提示码
	msg：				返回的提示信息
	error:				返回的错误的状态, 0无错误，1出错

<h3>2.21、	</h3><h3>单张图片上传接口</h3>  
【参数】  
>  
	
	Filedata		文件域【FILE】
	op				uploadphoto【照片上传】, uploadpic【日志的图片上传】
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=upload  
【返回值】  
>  
	
	data:
		picid:				图片id
		pic:				图片的url路径
		reward:
				credit:		返回的积分
		     experience：	返回的经验


<h3>2.22、	</h3><h3>发表照片接口</h3>  
【参数】  
>  
	
	message		照片描述
	picids		图片id, 多个用|连接(如：1|2|3)，调用2.21单张图片上传接口得到picid
	friend		查看范围：1家人可见，2仅自己可见，0全站用户可见
	tags		空间名
	friends		和谁在一起uid, 多个用|连接(如：1|2|3)  
	lat			纬度（客户端生成）
	lng			经度（客户端生成）
	address		发布地址（客户端生成）
	come		发布来源（客户端生成, iphone或者ipad或者android）
	makefeed	1, 是否产生feed
	makeweibo	是否发布到微博，1代表是
	makeqqweibo	是否发布到腾讯微博，1代表是
	photosubmit	1 如果设置了此变量，代表提交了数据  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=photo  
【返回值】  
>  
	
	data:
		credit:			返回的积分
		experience：	返回的经验
		id:				详情id
		idtype:			photoid
		uid:			发布人的uid
		oldid:			转发之前的id(转发才有值)

注：发布界面中还需要调用：  
2.32  [空间名称列表接口](#空间名称列表接口)  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 

<h3>2.23、	</h3><h3>转发照片接口</h3>  
【参数】  
>  
	
	photoid		照片id
	message		照片总体描述
	friend		查看范围：1家人可见，2仅自己可见，0全站用户可见
	tags		空间名
	friends		和谁在一起uid, 多个用|连接(如：1|2|3)  
	lat			纬度（客户端生成）
	lng			经度（客户端生成）
	address		发布地址（客户端生成）
	come		发布来源（客户端生成, iphone或者ipad或者android）
	makefeed	1, 是否产生feed
	makeweibo	是否发布到微博，1代表是
	makeqqweibo	是否发布到腾讯微博，1代表是
	photosubmit	1 如果设置了此变量，代表提交了数据,  无此变量代表是发布界面  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=rephoto  
【返回值】  
无photosubmit时，代表是发布的界面:  
>  
	
	data:
		photoid:		照片id
		message:		照片内容
		pic:			照片的图片
		countpic:		照片中包含的图片张数 
		
有photosubmit是，代表是提交了表单数据：  
>  
	
	data:
		credit:			返回的积分
		experience：	返回的经验
		id:				详情id
		idtype:			photoid
		uid:			发布人的uid
		oldid:			转发之前的id(转发才有值)

注：发布界面中还需要调用：  
2.32  [空间名称列表接口](#空间名称列表接口)  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 

<h3>2.24、	</h3><h3>发表日记接口</h3>  
【参数】  
>  
	
	subject		日志标题
	message		日志正文内容
	picids		图片id, 多个用|连接(如：1|2|3)，调用2.21单张图片上传接口得到picid
	friend		查看范围：1家人可见，2仅自己可见，0全站用户可见
	tags		空间名
	friends		和谁在一起uid, 多个用|连接(如：1|2|3)  
	lat			纬度（客户端生成）
	lng			经度（客户端生成）
	address		发布地址（客户端生成）
	come		发布来源（客户端生成, iphone或者ipad或者android）
	makefeed	1, 是否产生feed
	makeweibo	是否发布到微博，1代表是
	makeqqweibo	是否发布到腾讯微博，1代表是
	blogsubmit	1 如果设置了此变量，代表提交了数据，没有设置，那么就是发布界面  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=blog  
【返回值】  
>  
	
	data:
		credit:			返回的积分
		experience：	返回的经验
		id:				详情id
		idtype:			blogid
		uid:			发布人的uid
		oldid:			转发之前的id(转发才有值)

注：发布界面中还需要调用：  
2.32  [空间名称列表接口](#空间名称列表接口)  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 


<h3>2.25、	</h3><h3>转发日记接口</h3>  
【参数】  
>  
	
	blogid		被转发的日志id
	subject		日志标题
	message		日志正文内容
	picids		图片id, 多个用|连接(如：1|2|3)，调用2.21单张图片上传接口得到picid
	friend		查看范围：1家人可见，2仅自己可见，0全站用户可见
	tags		空间名
	friends		和谁在一起uid, 多个用|连接(如：1|2|3)  
	lat			纬度（客户端生成）
	lng			经度（客户端生成）
	address		发布地址（客户端生成）
	come		发布来源（客户端生成, iphone或者ipad或者android）
	makefeed	1, 是否产生feed
	makeweibo	是否发布到微博，1代表是
	makeqqweibo	是否发布到腾讯微博，1代表是
	blogsubmit	1 如果设置了此变量，代表提交了数据，没有设置，那么就是发布界面  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=reblog&blogid=被转的日志id  
【返回值】  
没有设置blogsubmit时, 即发布时的生成界面：  
>  
	
	data:
		blogid:			被转发的日志id
		subject:		日志标题
		message:		日志内容<html>
		其他参数与发布时提交参数含义一样

注：发布界面中还需要调用：  
2.32  [空间名称列表接口](#空间名称列表接口)  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 

设置了blogsubmit后，即提交了表单后：  
>  
	
	data:
		credit:			返回的积分
		experience：	返回的经验
		id:				详情id
		idtype:			blogid
		uid:			发布人的uid
		oldid:			转发之前的id(转发才有值)

<h3>2.26、	</h3><h3>发表活动接口</h3>  
【参数】  
>  
	
	title			活动标题
	location		活动地点
	starttime		活动开始时间
	classid			活动类型id
	detail			活动正文内容
	picids			图片id, 多个用|连接(如：1|2|3)，调用2.21单张图片上传接口得到picid
	friend			查看范围：1家人可见，2仅自己可见，0全站用户可见
	tags			空间名
	friends			和谁在一起uid, 多个用|连接(如：1|2|3)  
	lat				纬度（客户端生成）
	lng				经度（客户端生成）
	address			发布地址（客户端生成）
	come			发布来源（客户端生成, iphone或者ipad或者android）
	makefeed		1, 是否产生feed
	makeweibo		是否发布到微博，1代表是
	makeqqweibo	    是否发布到腾讯微博，1代表是
	eventsubmit		1 如果设置了此变量，代表提交了数据，没有设置，那么就是发布界面  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=event  
【返回值】  
>  
	
	data:
		credit:			返回的积分
		experience：	返回的经验
		id:				详情id
		idtype:			eventid
		uid:			发布人的uid
		oldid:			转发之前的id(转发才有值)

注：发布界面中还需要调用：  
2.28  [活动分类接口](#活动分类接口)  
2.32  [空间名称列表接口](#空间名称列表接口)  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 

<h3>2.27、	</h3><h3>转发活动接口</h3>  
【参数】  
>  
	
	title		活动标题
	location	活动地点
	starttime	活动开始时间
	classid		活动类型id
	detail		活动正文内容
	picids		图片id, 多个用|连接(如：1|2|3)，调用2.21单张图片上传接口得到picid
	friend		查看范围：1家人可见，2仅自己可见，0全站用户可见
	tags		空间名
	friends		和谁在一起uid, 多个用|连接(如：1|2|3)  
	lat			纬度（客户端生成）
	lng			经度（客户端生成）
	address		发布地址（客户端生成）
	come		发布来源（客户端生成, iphone或者ipad或者android）
	makefeed	1, 是否产生feed
	makeweibo	是否发布到微博，1代表是
	makeqqweibo	是否发布到腾讯微博，1代表是
	eventsubmit	1 如果设置了此变量，代表提交了数据，没有设置，那么就是发布界面   
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=reevent&eventid=被转发的活动id  
【返回值】  
没有设置eventsubmit时, 即发布时的生成界面：  
>  
	
	data:
		eventid:		被转发的活动id
		其他参数与发布时提交参数含义一样  

注：发布界面中还需要调用：  
2.28  [活动分类接口](#活动分类接口)  
2.32  [空间名称列表接口](#空间名称列表接口)  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 

设置了blogsubmit后，即提交了表单后：  
>  
	
	data:
		credit:			返回的积分
		experience：	返回的经验
		id:				详情id
		idtype:			eventid
		uid:			发布人的uid
		oldid:			转发之前的id(转发才有值)

<h3>2.28、	</h3><h3>活动分类接口</h3>  
【参数】[GET方式]  
m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=event&op=eventclass  
【返回值】  
>  
	
	data:
		eventclass 【活动分类数组】
			classid:	 	分类id
			classname：		分类名称
			template:		分类的内容描述模板


 
<h3>2.29、	</h3><h3>发表视频接口</h3>  
【参数】  
>  
	
	videourl	视频地址
	message		视频正文内容
	picids		图片id, 多个用|连接(如：1|2|3)，调用2.21单张图片上传接口得到picid
	friend		查看范围：1家人可见，2仅自己可见，0全站用户可见
	tags		空间名
	friends		和谁在一起uid, 多个用|连接(如：1|2|3)  
	lat			纬度（客户端生成）
	lng			经度（客户端生成）
	address		发布地址（客户端生成）
	come		发布来源（客户端生成, iphone或者ipad或者android）
	makefeed	1, 是否产生feed
	makeweibo	是否发布到微博，1代表是
	makeqqweibo	是否发布到腾讯微博，1代表是
	videosubmit	1 如果设置了此变量，代表提交了数据，没有设置，那么就是发布界面  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=video  
【返回值】  
>  
	
	data:
		credit:			返回的积分
		experience：	返回的经验  
		id:				详情id
		idtype:			videoid
		uid:			发布人的uid
		oldid:			转发之前的id(转发才有值)

注：发布界面中还需要调用：  
2.32  [空间名称列表接口](#空间名称列表接口)  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 

<h3>2.30、	</h3><h3>转发视频接口</h3>  
【参数】  
>   
	
	videourl	视频地址
	message		视频正文内容
	picids		图片id, 多个用|连接(如：1|2|3)，调用2.21单张图片上传接口得到picid
	friend		查看范围：1家人可见，2仅自己可见，0全站用户可见
	tags		空间名
	friends		和谁在一起uid, 多个用|连接(如：1|2|3)  
	lat			纬度（客户端生成）
	lng			经度（客户端生成）
	address		发布地址（客户端生成）
	come		发布来源（客户端生成, iphone或者ipad或者android）
	makefeed	1, 是否产生feed
	makeweibo	是否发布到微博，1代表是
	makeqqweibo	是否发布到腾讯微博，1代表是
	videosubmit	1 如果设置了此变量，代表提交了数据，没有设置，那么就是发布界面 
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
 
【调用方式】  
网站域名/dapi/cp.php?ac=video  
【返回值】  
没有设置videosubmit时, 即发布时的生成界面：  
>  
	

	data:
		videoid:		被转发的视频id  
		其他参数与发布时提交参数含义一样  

注：发布界面中还需要调用：  
2.32  [空间名称列表接口](#空间名称列表接口)  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 

设置了videosubmit后，即提交了表单后：  

	data:
		credit:			返回的积分
		experience：	返回的经验
		id:				详情id
		idtype:			videoid
		uid:			发布人的uid
		oldid:			转发之前的id(转发才有值)

<h3>2.31、	</h3><h3>发表我想说接口</h3>  
【参数】  
> 

		message		日志正文内容
		friends		和谁在一起uid, 多个用|连接(如：1|2|3)  
		lat			纬度（客户端生成）
		lng			经度（客户端生成）
		address		发布地址（客户端生成）
		come		发布来源（客户端生成, iphone或者ipad或者android）
		makeweibo	是否发布到微博，1代表是
		makeqqweibo	是否发布到腾讯微博，1代表是
		makefeed	是否生成动态，1代表是
		isaysubmit	1 如果设置了此变量，代表提交了数据，没有设置，那么就是发布界面  
		m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=isay  
【返回值】  
如果没有设置isaysubmit, 即发布界面上，得到的是默认的我说的句子列表：  
>  
		
		data:
			lid:		路上 句子列表 [数组]
			wid:		我说 句子列表 [数组]
		tid:			天气 句子列表 [数组]
		zid:			祝福 句子列表 [数组]

注：发布界面中还需要调用：  
2.33  [和谁在一起的人列表接口](#和谁在一起的人列表接口) 
  
点击发布后，即设置了isaysubmit，则返回值为：  
> 
	
	data:
		credit:			返回的积分
		experience：	返回的经验

<h3>2.32、	</h3><h3>空间名称列表接口</h3>  
【参数】【GET方式】  
m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=ajax&op=taglist    
【返回值】  
>  
	
	data
		taglist:【数组】  
			tagname	 	名称  



<h3>2.33、</h3><h3>和谁在一起的人列表接口</h3>  
【参数】【GET方式】  
m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=ajax&op=getfriend  
【返回值】  
>   

		data
			friendlist:	【数组】
				fuid		 	用户uid
				fusername		用户名
				favatar			用户头像
				vipstatus:		personal: 个人, family： 家庭， 空值：普通用户
				
<h3>2.34、</h3><h3>退出登录接口</h3>  
【参数】【GET方式】  
m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=logout  
【返回值】  
>   

		data
			return:  1  

 
<h3>2．35、	</h3><h3>家人分组接口</h3>  
【参数】  
>  
	
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=groupname&m_auth=?    
【返回值】  
>  
	
	data【数组】
			groupid		 	分组id  
			groupname		分组名称  
			

<h3>2．36、	</h3><h3>忽略/删除家人</h3>  
【参数】  
>

	uid:			被忽略或者被删除的家人的uid  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	friendsubmit    1 如果设置了此变量，代表提交了数据    
【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=ignore&uid=?&m_auth=?    
【返回值】  
>  
	 
	data
			return:  1  
			
<h3>2.37、	</h3><h3>删除对话接口</h3>  
【参数】  
>

	pmid			对话列表的id  
	deletesubmit	提交信息的表单验证，设为1即可   
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=pm&op=delete&folder=inbox&pmid=?&deletesubmit=1  
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错  
	
	
<h3>2.38、	</h3><h3>邀请注册接口</h3>  
【参数】  
>

	ac				invite  
	username		被邀请人的用户名(即手机号) 
	name			被邀请人的昵称 
	notename		被邀请人的备注名称 
	smsinvite		提交信息的表单验证，设为1即可   
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=invite&username=?&name=?&smsinvite=1  
【返回值】  
>  
	
	data
		password		被邀请人的登录密码  
		
		
<h3>2.39、	</h3><h3>表态类型接口</h3>  
【参数】  
>

	ac				click  
	op				clicktype
	idtype			类型(blogid,eventid,photoid,vedioid)
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=click&op=clicktype&idtype=?&m_auth=?   
【返回值】  
>  
	
	data 【数组】
		clickid		表情的id
		name		表情的名称
		icon		表情的图标
		idtype		表情所属的类型(blogid,eventid,photoid,vedioid)
		
<h3>2.40、	</h3><h3>修改密码接口</h3>  
【参数】  
>

	ac				account  
	password		当前密码 
	newpasswd1		新密码 
	newpasswd2		确认密码  
	pwdsubmit		提交信息的表单验证，设为1即可   
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=account 
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错  		
		
<h3>2.41、	</h3><h3>孩子资料修改接口</h3>  
【参数】  
>  
	
	babyname:			孩子姓名
	babysex:			孩子性别
	babybirthday:		孩子出生年月
	babyeditsubmit：	提交表单用的验证，设为1即可  
	babyid:				孩子id
	tagid:				空间详情id
	pic:				孩子头像url，调用2.21单张图片上传接口得到pic
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=baby  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错		
	
<h3>2.42、	</h3><h3>找回密码接口</h3>  
【参数】  
>  

	第一步：
	username:			用户名（手机号）
	lostpwsubmit:		提交表单用的验证，设为1即可  
	第二步：
	uid:			    第一步返回的uid
	newpasswd1:			新密码
	newpasswd2：		确认新密码
	code:				验证码
	resetsubmit:		提交表单用的验证，设为1即可
【调用方式】  
网站域名/dapi/do.php?ac=lostpasswd  
【返回值】  
>  

	第一步：
	data:
		uid:		用户uid
		username:	用户名
	
	
	第二步：
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错		
	
<h3>2.43、	</h3><h3>注册获取验证码接口</h3>  
【参数】  
>  

	username:			用户名（手机号）
【调用方式】  
网站域名/dapi/do.php?ac=register&op=getseccode&username=? 
【返回值】  
>  

	data
		seccode		验证码
		username	注册的用户名
		
		
<h3>2.44、	</h3><h3>删除日记/转发接口</h3>  
【参数】  
>  

	op			  delete   
	blogid		  日志id
	deletesubmit  1
	m_auth:		  API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=blog&op=delete   
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错		
		
<h3>2.45、	</h3><h3>删除活动/转发接口</h3>  
【参数】  
>  

	op			  delete   
	eventid		  活动id 
	deletesubmit  1
	m_auth:		  API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=event&op=delete   
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错				
	
	
<h3>2.46、	</h3><h3>删除视频/转发接口</h3>  
【参数】  
>  

	op			  delete   
	videoid		  视频id 
	deletesubmit  1
	m_auth:		  API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=video&op=delete   
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错	
		
<h3>2.47、	</h3><h3>删除照片/转发接口</h3>  
【参数】  
>  

	op			  delete   
	photoid		  照片id 
	deletesubmit  1
	m_auth:		  API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=photoid&op=delete   
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错			
		

<h3>2.48、	</h3><h3>绑定微博接口</h3>  
【参数】  
>  

	ac:				bindweibo
	type:			sina: 新浪微博, qq：腾讯微博  
	id:				微博的id
	token:			微博的token
	m_auth:		  	API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=bindweibo&type=?&id=?&token=?&m_auth=?  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错	

<h3>2.49、	</h3><h3>已读通知接口</h3>  
【参数】  
> 

	id		  	  通知id 
	m_auth:		  API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=notice  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错	
	
<h3>2.50、	</h3><h3>删除评论接口</h3>  
【参数】  
> 

	cid		  	  评论id
	uid			  被评论帖子的发布人的uid
	authorid	  评论人的uid
	m_auth:		  API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器 
	注意：帖子发布人可以删除该帖子下的任何一条评论，评论人只能删除自己的评论，
	客户端界面上应该会有所区分吧,请参考评论列表接口，新增了一个字段candel。
	
【调用方式】  
网站域名/dapi/cp.php?ac=delcomment 
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错	

<h3>2.51、	</h3><h3>删除转移空间的接口</h3>  
【参数】  
> 

	tagid		  	 需要删除的空间id
	totagid		  	 转移到的目标空间id【可选, 不填则只是删除，不转移】
	deletetagsubmit  1
	m_auth:		  	 API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=familyspace 
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错		
	
	
	
	