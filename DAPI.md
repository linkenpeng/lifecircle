 
**接口调用文档**

Author:  [Linkenpeng](mailto:collin_linken@qq.com)

[前言](#前言)

* 第一部分 [下行接口部分](#下行接口部分)
	* 1．1、	[获得周边小区接口](#获得周边小区接口)
	* 1．2、	[广告接口](#广告接口)
	* 1．3、	[动态列表接口](#动态列表接口)
	* 1．4、	[吐槽详情接口](#吐槽详情接口)
	* 1．5、	[获得分类接口](#获得分类接口)
	* 1．6、	[圈子吐槽详情接口](#圈子吐槽详情接口)
	* 1．7、	[圈子列表接口](#圈子列表接口)
	* 1．8、	[圈子吐槽列表接口](#圈子吐槽列表接口)
	* 1．9、	[评论列表接口](#评论列表接口)
	* 1．10、[个人空间接口](#个人空间接口)
	* 1．11、[对话列表接口](#对话列表接口)
	* 1．12、[对话详情接口](#对话详情接口)
	* 1．13、[通知列表接口](#通知列表接口)
	* 1．14、[个人设置读取接口](#个人设置读取接口)
	* 1．15、[好友列表接口](#好友列表接口)
	* 1．16、[好友分组接口](#好友分组接口)
	* 1．17、[好友添加申请列表接口](#好友添加申请列表接口)
	
	
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

注(请仔细阅读)：  
	
	1)	下行接口中，除非标注有POST方式，否则一律用GET方式请求数据。  
	2)	上行接口中，除非标注有GET方式，否则一律用POST方式发送数据。  
	3)	在上行接口中，包含有部分下行接口，用来生成发布界面。  
	4)  所有接口中，需要发送一个【m_auth】【登录时获得】的参数，进行认证，除非是特别强调不需要登录验证的接口。
	5)	如果服务器返回：
		data: {
			return: -1
		},
		msgkey: auth_failure
		msg: auth_failure
		error: 1
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

		data: {
			adid: 2
			title: 手机广告
			imagesrc: http://www.baidu.com/img/baidu_sylogo1.gif
			idtype: blog
			id: 1
		},
		msgkey: rest_success
		msg: 数据获取成功
		error: 0
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
	pagetype:		页面位置
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
	xiaoquid: 小区id
	
	以下参数暂时不用管 
	longitude: 发布经度
	latitude: 0.0000000000	
	icon: friend
	friend: 0
	target_ids: 
	body_general: 
	append_idtype: 
	append_id: 0
	append_text: 
	append_title: 
	append_link: 
	append_image: 
	replynum: 0
	forwardnum: 0
	goodnum: 0	
	hot: 0
	istop: 0	
	tag: 
	
1.4、<h3>吐槽详情接口</h3>  
【参数】  
>

	talkid:	 吐槽主键id

【调用方式】  
网站域名/dapi/space.php?do=talk  
【返回值】  
> 

	talkid: 吐槽id【主键】
	uid: 发表吐槽人uid
	username: 吐槽人用户名
	name: 吐槽人真实名字
	avatar: 吐槽人头像
	classid: 分类id
	xiaoquid: 小区id	
	title: 吐槽标题
	message: 吐槽内容
	from: 发布来源，如：iphone/android/ipad/web
	tag: 标签	
	images: 图片【数组】
	location: 发布地址
	dateline: 发布时间戳	
	
	以下参数暂时不用管
	longitude: 0.0000000000
	latitude: 0.0000000000
	append_idtype: 
	append_id: 0
	append_text: 
	append_title: 
	append_link: 
	append_image: 
	picids: 87,88,89
	ip: 192.168.1.138
	replynum: 0
	forwardnum: 0
	goodnum: 0
	friend: 0	
	
1.5、<h3>获得分类接口</h3>  
【参数】  
无
【调用方式】  
网站域名/dapi/space.php?do=taglist  
【返回值】  
> 

	数组:  
	tagid: 	 分类id
	tagname: 分类名
	
1.6、<h3>圈子吐槽详情接口</h3>  
【参数】  
>

	id:	 	圈子吐槽主键id

【调用方式】  
网站域名/dapi/space.php?do=mtalk  
【返回值】  
> 

	mtalkid: 圈子吐槽主键id
	uid: 吐槽人uid
	username: 吐槽人用户名
	name: 吐槽人真实名字
	avatar: 吐槽人头像
	tagid: 标签id
	xiaoquid: 小区id
	classid: 分类id		
	title: 标题
	message: 内容
	images: 图片数组
	show_good: 赞的人数组
	commentlist: 评论数组
	from: 发布来源
	location: 发布地址
	dateline: 发表的时间戳
	
	以下参数暂时不用管
	append_type: none
	append_author: 
	append_text: 
	append_title: 
	append_image: 
	pics: a:0:{}
	forwardid: 0
	pre_forwardid: 0
	ip: 127.0.0.1
	replynum: 0
	forwardnum: 0
	goodnum: 0	
	longitude: 0.0000000000
	latitude: 0.0000000000
	
1.7、<h3>圈子列表接口</h3>  
【参数】  
>

	xiaoquid: 	小区id

【调用方式】  
网站域名/dapi/space.php?do=mtag  
【返回值】  
> 
	
	数组：
		tagid: 圈子id
		tagname: 圈子名
		membernum: 成员数		
		talknum: 圈子吐槽数
		topimages: 图片数组
		close: 圈子开启状态：0 开启 1 关闭
		grade: 允许参与的用户组	
		
		以下参数暂时不用管
		postnum: 0
		uid: 1
		username: admin		
		fieldid: 1
		xiaoquid: 1	
		threadnum: 帖子数			
		announcement: 没公告……不知道说啥
		pic: 
		closeapply: 0
		joinperm: 0
		viewperm: 0
		threadperm: 0
		postperm: 0
		recommend: 0
		moderator: 	
		title: 其他	

1.8、<h3>圈子吐槽列表接口</h3>  
【参数】  
>

	tagid: 	 圈子id 
	page:	 当前页【默认1】
	perpage: 每页数量【默认10】
	keyword: 搜索关键词【默认为空】

【调用方式】  
网站域名/dapi/space.php?do=mtalk&op=talklist  
【返回值】  
> 
	
	数组：
		mtalkid: 圈子吐槽主键id
		uid: 吐槽人uid
		username: 吐槽人用户名
		name: 吐槽人真实名字
		avatar: 吐槽人头像	
		title: 标题
		message: 内容
		images: 图片数组
		show_good: 赞的人数组
		commentlist: 评论数组
		from: 发布来源
		location: 发布地址
		dateline: 发表的时间戳
		tagid: 圈子id
		xiaoquid: 小区id	
		
		以下参数暂时不用管
		classid: 0		
		append_idtype: 
		append_id: 0
		append_uid: 0
		append_text: 
		append_title: 
		append_image: 
		append_link: 
		pics: a:0:{}
		ip: 127.0.0.1
		replynum: 0
		forwardnum: 0
		goodnum: 0		
		longitude: 0.0000000000
		latitude: 0.0000000000
		
<h3>1．9、	</h3><h3>评论列表接口</h3>  
【参数】  
>  

	id:			被评论的对象id
	idtype:		被评论的类型(photoid: 照片, 'blogid'：日志)
	page:		当前页，默认1
	perpage:	每页数量，默认10
	starttime:	取数据的开始时间，不包含变量自身, 默认空值不设置数据范围 
	endtime:	取数据的结束时间，不包含变量自身, 默认空值不设置数据范围

【调用方式】  
网站域名/dapi/space.php?do=comment  
【返回值】  
>  

	cid:			评论主键id
	authorid:		评论用户uid
	avatar:			头像url
	authorname:		评论用户名
	message:		评论内容
	dateline:		评论时间
	candel:			是否有删除权限，1：有 0：无		

<h3>1．10、	</h3><h3>个人空间接口</h3>  
【参数】  
>  

	uid:			空间主人的uid【为空则是登录人的uid】

【调用方式】  
网站域名/dapi/space.php  
【返回值】  
>  

	uid: 用户id
	username: 用户名
	nickname: 昵称
	name: 真实名字
	mobile: 手机号
	idcard: 身份证
	verifystatus: 认证状态：0 未认证；1等待审核；2通过审核	
	avatar: 头像
	friendnum: 好友数
	talknum: 吐槽数
	verify_type: 认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	
	以下参数暂时不用管
	namestatus: 1
	sex: 男
	email: 
	newemail: 
	emailcheck: 0
	mobile2: 18028056032
	qq: 153008910
	msn: 
	msnrobot: 
	msncstatus: 0
	videopic: 
	birthyear: 1986
	birthmonth: 11
	birthday: 11
	blood: O
	marry: 非单身
	birthprovince: 广东
	birthcity: 广东江门
	resideprovince: 广东
	residecity: 广东广州
	note: 
	spacenote: 
	authstr: 
	theme: t12
	nocss: 0
	menunum: 0
	css: 
	privacy: {
		view: {
			index: 0
			profile: 0
			friend: 0
			wall: 0
			feed: 0
			mtag: 0
			event: 0
			doing: 0
			blog: 0
			album: 0
			share: 0
			poll: 0
		},
		feed: {
			doing: 1,
			blog: 1,
			upload: 1,
			share: 1,
			poll: 1,
			joinpoll: 1,
			thread: 1,
			post: 1,
			mtag: 1,
			event: 1,
			join: 1,
			friend: 1,
			comment: 1,
			show: 1,
			spaceopen: 1,
			credit: 1,
			invite: 1,
			task: 1,
			profile: 1,
			album: 1,
			click: 1
		}
	},
	friend: 2,6
	feedfriend: 2,6
	sendmail: 
	magicstar: 0
	magicexpire: 0
	timeoffset: 
	xiaoquid: 1
	groupid: 1
	credit: 765
	experience: 879	
	roomid: 36	
	videostatus: 0
	neighbor_verify_num: 0
	domain: 	
	viewnum: 18
	notenum: 1
	addfriendnum: 1
	mtaginvitenum: 0
	eventinvitenum: 0
	myinvitenum: 0
	pokenum: 0
	doingnum: 0	
	blognum: 1
	albumnum: 1
	threadnum: 1
	pollnum: 1
	eventnum: 0
	sharenum: 2
	dateline: 1369763493
	updatetime: 1377527332
	lastsearch: 0
	lastpost: 1377527332
	lastlogin: 1377526289
	lastsend: 0
	attachsize: 6654532
	addsize: 0
	addfriend: 0
	flag: 1
	newpm: 0	
	regip: 127.0.0.1
	ip: 127000000
	mood: 18
	myapp: 1,2,3,4
	self: 1,
	xiaoqu: {
		xiaoquid: 1
		xiaoquname: 华南御景园
		uid: 1
		username: admin
		introduce: 这里环境优美啊，空气好啊……就是路太烂。
		pic_url: http://shq-pic.b0.upaiyun.com/201307/2/1_1372733067xKkX.jpg
		usernum: 0
		locationid: 5
		longitude: 113.3787200000
		latitude: 23.1710100000
		citycode: 101280101
	},
	friends: [
		2
		6
	],
	allnotenum: 2,
	isfriend: 1,
	sex_org: 1
	birth: 1986年11月11日
	star: <img src=\image/star_level2.gif\ align=\absmiddle\ />
	domainurl: http://my.life.com/dapi/?1
	magiccredit: 0,
	userapp: []

<h3>1．11、	</h3><h3>对话列表接口</h3>  
【参数】  
>  

	page		当前页【默认1】
	perpage		每页数量【默认10】

【调用方式】  
网站域名/dapi/space.php?do=pm  
【返回值】  
>  

	plid: 对话主键id
	authorid: 发起人uid
	authorname: 发起人名字
	authorvavatar: 发起人头像
	subject: 发起时主题
	founddateline: 发起时间戳
	lastsummary: 最后回复时间
	lastauthorid: 最后回复人uid
	lastauthorname: 最后回复人名字
	lastdateline: 最后回复时间
	msgtoid: 对话对方的uid
	isnew: 是否是新的对话，1：是 0：不是
	pmnum: 对话详情内容数量
	touid: 对话对方的uid	
	
	以下参数暂时不用管
	uid: 1		
	lastupdate: 1377609063	
	pmtype: 1	
	members: 2
	dateline: 1377609063
	lastmessage: a:3:{s:12:\lastauthorid\;s:1:\1\;s:10:\lastauthor\;s:5:\admin\;s:11:\lastsummary\;s:7:\回复1\;}
	pmid: 3	
	lastauthor: admin	
	msgfromid: 1
	msgfrom: admin
	message: 回复1
	new: 0	
	daterange: 1,
	tousername: linken

<h3>1．12、	</h3><h3>对话详情接口</h3>  
【参数】  
>  

	plid 	对话列表中的主键id
	touid	对话列表中的touid

【调用方式】  
网站域名/dapi/space.php?do=pm&subop=view  
【返回值】  
>  
	
	plid: 3	
	msgfromid: 发信人uid
	msgfrom: 发信人用户名
	msgfromname: 发信人名称
	msgfromavatar: 发信人头像	
	message: 信息内容
	msgtoid: 收信息人uid	
	msgtoname: 收信息人名字
	msgtoavatar: 收信息人的头像
	dateline: 信息生成时间戳
	
	以下参数暂时不用管
	authorid: 6
	author: linken
	pmtype: 1
	subject: 对话1
	members: 2	
	pmid: 5	
	founderuid: 6
	founddateline: 1377609043
	touid: 1
	
<h3>1．13、	</h3><h3>通知列表接口</h3>  
【参数】  
>  

	page 	当前页【默认1】
	perpage	每页数量【默认10】

【调用方式】  
网站域名/dapi/space.php?do=notice  
【返回值】  
>  
	
	id: 通知主键id	
	new: 是否是新的通知 1：是 0：不是
	authorid: 产生通知人的uid
	author: 产生通知人的用户名
	authorname: 产生通知人的名字
	authoravatar: 产生通知人的头像
	isfriend: 产生通知的人是否是自己的好友 1 ：是		
	note: 评论内容
	dateline: 通知时间戳
	idtype: 帖子的类型，如：blogid
	sid: 帖子的id

	以下参数暂时不用管
	uid: 接收通知人的uid
	type: 通知类型
	
<h3>1．14、	</h3><h3>个人设置读取接口</h3>  
【参数】  
>  

	无

【调用方式】  
网站域名/dapi/cp.php?ac=profile  
【返回值】  
>  
	
	uid: 用户uid
	username: 用户名
	name: 用户实名
	avatar: 用户头像
	mobile: 手机号
	verifystatus: 认证状态：0 未认证；1等待审核；2通过审核
	xiaoquname: 小区名
	qiname: 期
	dongname: 栋
	cengname: 层
	roomname: 室
	
<h3>1．15、	</h3><h3>好友列表接口</h3>  
【参数】  
>  

	group:   分组id
	page:	 当前页【默认1】
	perpage: 每页数量【默认10】

【调用方式】  
网站域名/dapi/space.php?do=friend  
【返回值】  
>  
	
	uid:      用户uid
	username: 用户名
	name:     用户实名
	avatar:   用户头像
	note:     好友备注
	
<h3>1．16、	</h3><h3>好友分组接口</h3>  
【参数】  
>  

	无

【调用方式】  
网站域名/dapi/space.php?do=friend&view=groupname  
【返回值】  
>  
	
	数组
		gid: 分组id
		gname: 分组名称
		
<h3>1．17、	</h3><h3>好友添加申请列表接口</h3>  
【参数】  
>  

	无

【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=request  
【返回值】  
>  
	
	uid: 用户uid
	username: 用户名
	avatar: 用户头像
	name: 用户实名
	verifystatus: 认证状态：0 未认证；1等待审核；2通过审核
	dateline: 申请时间戳
	
	以下参数暂时不用管
	mobile: 手机号	
	xiaoquid: 用户所在小区id
	groupid: 用户分组id	
	credit: 105
	experience: 95
	nickname: 测试用户	
	idcard: 111111111111111111
	roomid: 21	
	namestatus: 1
	videostatus: 0
	neighbor_verify_num: 0
	domain: 
	friendnum: 0
	viewnum: 1
	notenum: 2
	addfriendnum: 0
	mtaginvitenum: 0
	eventinvitenum: 0
	myinvitenum: 0
	pokenum: 0
	doingnum: 0
	talknum: 0
	blognum: 0
	albumnum: 0
	threadnum: 0
	pollnum: 0
	eventnum: 0
	sharenum: 0	
	updatetime: 1374045850
	lastsearch: 0
	lastpost: 1377098373
	lastlogin: 1377312996
	lastsend: 0
	attachsize: 0
	addsize: 0
	addfriend: 0
	flag: 0
	newpm: 0	
	regip: 127.0.0.1
	ip: 127000000
	mood: 0
	myapp: null,
	friend: 
	fuid: 1
	fusername: admin
	status: 0
	gid: 5
	note: 
	num: 0
	cfriend: 
	cfcount: 0
	
	

	
<h2>第二部分 </h2><h2>上行接口部分</h2>
==================

<h3>2.1、	</h3><h3>注册获取验证码接口</h3>  
【参数】  
>  

	username:			用户名（手机号）
【调用方式】【GET方式】  
网站域名/dapi/do.php?ac=register&op=getseccode   
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
	xiaoquid:		调用 1.1、获得周边小区接口 供用户选择xiaoquid
	
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
					verify_type:   0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
					is_sina_bind 是否绑定新浪微博 1 是 0 否  
					is_qq_bind   是否绑定腾讯微博 1 是 0 否  
					

<h3>2.3、	</h3><h3>普通登录接口</h3>  
【参数】  
>  

	username:		账号
	password:		密码
	iscookie:		是否保存密码，为1时保存 
	
【调用方式】  
网站域名/dapi/do.php?ac=login  
【返回值】  
>  
	
	data:
	 return: 返回的状态码，
			-1： 用户名或者密码为空
			-2： 用户名或者密码错误
			 1： 登录成功
	 m_auth:      登录成功后返回的登录密匙，请求每个接口都需要发送这个参数给服务器,重新登录时，这个值会改变。
	 uid:	      用户的uid  
	 username: 	  用户名  
	 name:     	  用户昵称  
	 avatar:      用户头像  
	 credit：     本次登录的积分
	 experience   本次登录的经验
	 is_sina_bind 是否绑定新浪微博 1 是 0 否
	 is_qq_bind   是否绑定腾讯微博 1 是 0 否
	 verify_type:   0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	 xiaoquid:		小区id
	 
<h3>2.4、	</h3><h3>第三方登录接口</h3>  
【参数】  
>  
	
	以下参数二选一：
	新浪微博登录
	logintype:			weibo	
	name:				新浪微博昵称 
	sina_uid			新浪微博的uid 	
	sina_token			新浪微博token  
	sina_expires_in		新浪微博token过期时间(格式：2013-05-12 22:59:59) 
	
	腾讯微博登陆 
	logintype:			qq  		
	name:				腾讯微博的昵称 
	qq_openid			腾讯微博的id  
	qq_token			腾讯微博token 
	
	如果用户未绑定，后台会自动用参数进行注册并登录。已经绑定的，直接登录。
	
【调用方式】  
网站域名/dapi/do.php?ac=login  
【返回值】  
>  
	
	data:
		return:	返回的状态码
			-1：token的uid参数为空
			-2：token的uid未绑定
			 1：登录成功
		m_auth:      登录成功后返回的登录密匙，请求每个接口都需要发送这个参数给服务器,重新登录时，这个值会改变  
		uid:	     用户的uid  
		username:    用户名  
		name:        用户昵称  
		avatar:      用户头像  
		credit：     本次登录的积分
		experience   本次登录的经验
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
	
	
	
	
	
	