 
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

<h3>注(请仔细阅读)</h3>：

	1)	下行接口中，除非标注有POST方式，否则一律用GET方式请求数据。  
	2)	上行接口中，除非标注有GET方式，否则一律用POST方式发送数据。  
	3)	在上行接口中，包含有部分下行接口，用来生成发布界面。  
	4)  所有接口中，需要发送一个【m_auth】【登录时获得】的参数，进行认证，除非是特别强调不需要登录验证的接口。
	5)	如果服务器返回：
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

1.1、<h3>获得周边小区接口</h3>  
【参数】  
>

	keyword:	小区名称
	longitude:  小区经度
	latitude:   小区维度
	span:		经纬度范围【默认0.01】

【调用方式】  
网站域名/dapi/do.php?ac=xiaoqu&op=getlist
【返回值】  
> 

	xiaoquid: 	小区id
	xiaoquname: 小区名字
	uid: 		发布人uid
	username: 	发布人用户名
	name: 		发布人名字
	avatar: 	发布人用户名
	introduce:  小区简介
	pic_url: 	小区图片
	usernum: 	小区用户数
	locationid: 地区id
	longitude:  小区经度
	latitude: 	小区维度
	citycode: 	天气网城市代码

1.2、<h3>广告接口</h3>  
【参数】  
>

	xiaoquid:	小区id

【调用方式】  
网站域名/dapi/space.php?do=ad
【返回值】  
> 

	adid: 			广告id
	xiaoquid: 		广告id
	title: 			广告标题
	imageheight: 	图片高度
	imagewidth: 	图片宽度
	imagesrc: 		图片url地址
	imageurl: 		广告链接到的地址
  		
1.3、<h3>动态列表接口</h3>  
【参数】  
>

	xiaoquid:	小区id【默认为空】
	classid:	分类id【默认为空】
	page:		当前页【默认1】
	perpage:	每页数量【默认10】
	uid:		用户uid【默认为登录用户的uid】
	keyword		关键词搜索【默认为空】

【调用方式】  
网站域名/dapi/space.php?do=home  
【返回值】  
> 

	uid: 用户id
	username: 用户名
	name: 用户实名
	avatar: 用户头像
	titile: 动态标题
	content: 动态内容
	id: 帖子的id
	idtype: 帖子的id类型,如：blogid/photoid/talkid
	classid: 分类id
	images: 动态图片数组
	comment: 动态的评论
	showgood: 动态赞的人
	from: 发布来源，如：web/iphone/ipad/android/winphone	
	location: 发布地址 
	dateline: 动态产生的时间戳 
	
	以下参数暂时不知道用处 
	longitude: 发布经度
	latitude: 0.0000000000
	xiaoquid: 1	
	icon: friend
	friend: 0
	target_ids: 
	body_general: 
	append_type: none
	append_author: 
	append_text: 
	append_title: null,
	append_link: null,
	append_image: null,
	forwardid: 0
	replynum: 0
	forwardnum: 0
	goodnum: 0	
	hot: 0
	istop: 0	
	tag: 
	

	

		
<h2>第二部分 </h2><h2>上行接口部分</h2>
==================

<h3>2.1、	</h3><h3>注册获取验证码接口</h3>  
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
		
<h3>2.2、	</h3><h3>注册接口</h3>  
【参数】  
>  
	
	注册前调用 2.1、注册获取验证码接口
	
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
					

<h3>2.3、	</h3><h3>普通登录接口</h3>  
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
	 
<h3>2.4、	</h3><h3>第三方登录接口</h3>  
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

 
<h3>2.5、	</h3><h3>找回密码接口</h3>  
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

<h3>2.6、</h3><h3>退出登录接口</h3>  
【参数】【GET方式】  
m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=logout  
【返回值】  
>   

		data
			return:  1  
	
	
	
	
	
	