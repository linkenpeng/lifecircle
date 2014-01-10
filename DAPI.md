 
**接口调用文档**

Author:  [ChanYu Leung](mailto:269226841@qq.com)

[前言](#前言)

* 第一部分 [下行接口部分](#下行接口部分)
	* 1．1.01、	[获得周边小区接口](#获得周边小区接口)
	* 1．1.02、	[获得推荐小区接口](#获得推荐小区接口)
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
	* 1．18、[赞列表接口](#赞列表接口)
	* 1．19、[推荐好友接口](#推荐好友接口) 
	* 1．20、[获取小区物业分布信息（期、栋、层、房号）接口](#获取小区物业分布信息（期、栋、层、房号）接口) 
	* 1．21、[便民列表接口](#便民列表接口)  
	* 1．22、[未处理消息数量接口](#未处理消息数量接口)  
	* 1．23、[小区周边商家接口](#小区周边商家接口)  
	* 1．24、[查询该月份是否已经发布账单接口](#查询该月份是否已经发布账单接口)  
	* 1．25、[查询该月份该房间是否已经发布账单接口](#查询该月份该房间是否已经发布账单接口)  
	* 1．26.01、[获得房间ID接口](#获得房间ID接口)  
	* 1．26.02、[通过地址获得房间ID接口](#通过地址获得房间ID接口)  
	* 1．26.03、[获得所有房间ID接口](#获得所有房间ID接口)  
	* 1．27、[搜索小区接口](#搜索小区接口)  
	* 1．28、[未读通知数接口](#未读通知数接口)  
	* 1．29、[一个圈子信息的接口](#一个圈子信息的接口)  
	
		
	
* 第二部分 [上行接口部分](#上行接口部分)  
	* 2.1、	[注册获取验证码接口](#注册获取验证码接口)  
	* 2.2、	[注册接口](#注册接口)  
	* 2.3、 [普通登录接口](#普通登录接口)  
	* 2.4、	[第三方登录接口](#第三方登录接口)  
	* 2.5、	[找回密码接口](#找回密码接口)  
	* 2.6、	[退出登录接口](#退出登录接口)  
	* 2.7、	[赞接口](#赞接口)   
	* 2.8、	[修改头像接口](#修改头像接口)   
	* 2.9、	[修改昵称接口](#修改昵称接口)   
	* 2.10、	[申请成为好友接口](#申请成为好友接口)  
	* 2.11、	[同意成为好友接口](#同意成为好友接口)  
	* 2.12、	[发私信接口](#发私信接口)  
	* 2.13、	[发表/转发吐槽接口](#发表/转发吐槽接口)  
	* 2.14、	[上传照片接口](#上传照片接口)  
	* 2.15、	[设置吐槽分类接口](#设置吐槽分类接口)  
	* 2.16、	[申请加入圈子接口](#申请加入圈子接口)  	
	* 2.17、	[退出圈子接口](#退出圈子接口)  	
	* 2.18、	[发表圈子吐槽接口](#发表圈子吐槽接口)  	
	* 2.19.00、	[发表评论接口](#发表评论接口)  	
	* 2.19.01、	[回复评论接口](#回复评论接口)  	
	* 2.19.02、	[删除评论接口](#删除评论接口)  	
	* 2.20、	[个人基本设置保存接口](#个人基本设置保存接口)  	
	* 2.21、	[个人认证信息保存接口](#个人认证信息保存接口)  		
	* 2.22、	[取消好友关注接口](#取消好友关注接口)  		
	* 2.23、	[修改密码接口](#修改密码接口)  	
	* 2.24、	[提交账单接口](#提交账单接口)  	
	* 2.25、	[注册时更新小区id接口](#注册时更新小区id接口)  
	* 2.26、	[设置主题图片接口](#设置主题图片接口)  
	* 2.27、	[发布商品接口](#发布商品接口)  
	
 
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

1.1.01、<h3>获得周边小区接口</h3>  
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

1.1.02、<h3>获得推荐小区接口</h3>  
【参数】  
>

	keyword:	小区名称

【调用方式】  
网站域名/dapi/do.php?ac=xiaoqu&op=getrecommendlist
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
	pagetype:	页面位置
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

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
	idtype		动态类型，如blogid,talkid等【默认全部】
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=home  
【返回值】  
> 
data:数组
	uid: 用户id
	username: 用户名
	name: 用户实名
	avatar: 用户头像
	verify_type:   0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	title: 动态标题
	titile: 和title一样，这是错误的拼写，以后会除去
	content: 动态内容
	id: 帖子的id
	idtype: 帖子的id类型,如：blogid/photoid/talkid
	classid: 分类id
	images: 动态图片数组
		small:缩略图，150x150
		mid:缩放图，如果宽度大于长度，则宽度为310，高度自适应。反之亦然
		big:原图
		width:图片宽度
		height:图片高度
	comment: 动态的评论
	showgood: 动态赞的人
	isshowgood:是否已经赞过（是：1，否：0）
	from: 发布来源，如：web/iphone/ipad/android/winphone	
	location: 发布地址 
	dateline: 动态产生的时间戳 
	xiaoquid: 小区id
	share_url:		分享到微信的连接
	feedtype:0：系统类型、1：吐槽原帖、2：转发吐槽（和附件样式一样）、3：附件（例如二手商品）、4：转发附件（例如转发二手商品）
	append_idtype: 
	append_id: 附件id
	append_text: 
	append_title: 
	append_link: 
	append_image: 附件图片
	append_image_width:附件图片宽度
	append_image_height:附件图片高度


	
	以下参数暂时不用管 
	longitude: 发布经度
	latitude: 0.0000000000	
	icon: friend
	friend: 0
	target_ids: 
	body_general: 
	replynum: 0
	forwardnum: 0
	goodnum: 0	
	hot: 0
	istop: 0	
	tag: 

	other:数组
	pic_url :小区主题图片


1.4、<h3>吐槽详情接口</h3>  
【参数】  
>

	talkid:	 吐槽主键id
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=talk  
【返回值】  
> 

	talkid: 吐槽id【主键】
	id:和talkid一样
	uid: 发表吐槽人uid
	username: 吐槽人用户名
	name: 吐槽人真实名字
	avatar: 吐槽人头像
	verify_type:   0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	classid: 分类id
	xiaoquid: 小区id	
	title: 吐槽标题
	message: 吐槽内容
	from: 发布来源，如：iphone/android/ipad/web
	tag: 标签	
	images: 图片【数组】
		big:
		mid:
		small:
		width:
		height:
	location: 发布地址
	dateline: 发布时间戳	
	showgood: 赞的人数组
	comment: 评论数组
	
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
>

	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
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

	id:	 		圈子吐槽主键id
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=mtalk  
【返回值】  
> 

	mtalkid: 圈子吐槽主键id
	id:和mtalkid一样
	uid: 吐槽人uid
	username: 吐槽人用户名
	name: 吐槽人真实名字
	avatar: 吐槽人头像
	verify_type:   0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	tagid: 标签id
	xiaoquid: 小区id
	classid: 分类id		
	title: 标题
	message: 内容
	images: 图片数组
	showgood: 赞的人数组
	show_good: 与showgood一样，为错误拼写，以后除去
	comment: 评论数组
	commentlist: 与comment一样，为错误拼写，以后除去
	from: 发布来源
	location: 发布地址
	dateline: 发表的时间戳
	iamges:数组
		"big"
		"mid"
		"small"
	
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
	page:		分页数【默认1】
	perpage:	每页数【默认10】
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

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
		pic:圈子主题图片

		以下参数暂时不用管
		postnum: 0
		uid: 1
		username: admin		
		fieldid: 1
		xiaoquid: 1	
		threadnum: 帖子数			
		announcement: 没公告……不知道说啥
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
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=mtalk&op=talklist  
【返回值】  
> 
	data:
		pic:圈子主题图片
		list:数组
			mtalkid: 圈子吐槽主键id
			id:和mtalkid一样
			uid: 吐槽人uid
			username: 吐槽人用户名
			name: 吐槽人真实名字
			avatar: 吐槽人头像	
			verify_type:   0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
			title: 标题
			message: 内容
			images: 图片数组
			showgood: 赞的人数组
			comment: 评论数组
			from: 发布来源
			location: 发布地址
			dateline: 发表的时间戳
			tagid: 圈子id
			xiaoquid: 小区id	
			isshowgood:		  是否已经赞过（是：1，否：0）
			isShowgood:		  和isshowgood一样，这是错误拼写，以后会除去。
			share_url:		分享到微信的连接
			append_idtype: 附件类型
			append_id: 附件id
			append_uid: 
			append_text: 
			append_title: 
			append_image: 附件图片
			append_image_width:附件图片宽度
			append_image_height:附件图片高度 
			append_link: 
			append_mtalkid: 


			以下参数暂时不用管
			classid: 0		
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
	idtype:		被评论的类型(talkid: 吐槽, 'blogid'：日志)
	page:		当前页，默认1
	perpage:	每页数量，默认10
	starttime:	取数据的开始时间，不包含变量自身, 默认空值不设置数据范围 
	endtime:	取数据的结束时间，不包含变量自身, 默认空值不设置数据范围
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=comment  
【返回值】  
>  

	cid:				评论主键id
	authoruid:			评论用户uid
	authoravatar:		头像url
	authorverify_type:  0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	authorname:			评论用户昵称
	authorusername:		评论用户名
	message:			评论内容
	dateline:			评论时间
	candel:				是否有删除权限，1：有 0：无		

<h3>1．10、	</h3><h3>个人空间接口</h3>  
【参数】  
>  

	uid:		空间主人的uid【为空则是登录人的uid】
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php  
【返回值】  
>  

	uid: 	  	  用户id
	username: 	  用户名
	name: 	  	  用户昵称
	realname: 	  用户实名
	mobile:   	  手机号
	idcard:   	  身份证
	verifystatus: 认证状态：0 未认证；1等待审核；2通过审核；-1审核不通过
	avatar: 	  头像
	friendnum:    好友数
	talknum:      吐槽数
	verify_type:  认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	mtagnum:	  圈子数  
	lovenum:	  收藏数  
	themepic:	 
			original:	原图
			adapt:		主题图缩略图
	privacy：隐私【数组】
			birthcity	家乡隐私 0：全用户可见 3: 仅自己可见
			birth		生日隐私 0：全用户可见 3: 仅自己可见
			qq			qq隐私 0：全用户可见 3: 仅自己可见
			marry		婚姻状态隐私 0：全用户可见 3: 仅自己可见
			mobile		手机隐私 0：全用户可见 3: 仅自己可见
			sex			性别隐私 0：全用户可见 3: 仅自己可见
	
	verify_type=3时，即商家认证
	couponslist【优惠券数组】
		cid:		优惠券id
		subject:	优惠券名字
		pic:		优惠券图片
	couponslist【商品数组】
		goodsid:	商品id
		subject:	商品名字
		pic:		商品图片
		
	
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
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=pm  
【返回值】  
>  

	plid: 					对话主键id
	authoruid: 				发起人uid
	authorname: 			发起人名字
	authorvavatar: 			发起人头像
	authorverify_type:  	认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	subject: 				发起时主题
	founddateline: 			发起时间戳
	lastsummary: 			最后回复时间
	lastauthoruid: 			最后回复人uid
	lastauthorname: 		最后回复人名字
	lastauthorverify_type:  认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	lastdateline: 			最后回复时间
	msgtoid: 				对话对方的uid
	isnew: 					是否是新的对话，1：是 0：不是
	pmnum: 					对话详情内容数量
	touid: 					对话对方的uid	
	
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
	m_auth:	API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=pm&subop=view  
【返回值】  
>  
	
	plid: 				对话详情主键id	
	msgfromuid: 		发信人uid
	msgfrom: 			发信人用户名
	msgfromname: 		发信人名称
	msgfromavatar: 		发信人头像	
	msgfromverify_type: 认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	message: 			信息内容
	msgtouid: 			收信息人uid	
	msgtoname: 			收信息人名字
	msgtoavatar: 		收信息人的头像
	msgtoverify_type:  	认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	dateline: 			信息生成时间戳
	
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

	page 		当前页【默认1】
	perpage		每页数量【默认10】
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=notice  
【返回值】  
>  
	
	id: 			通知主键id	
	new: 			是否是新的通知 1：是 0：不是
	authoruid: 		产生通知人的uid
	authorusername: 产生通知人的用户名
	authorname: 	产生通知人的名字
	authoravatar: 	产生通知人的头像
	authorverify_type:认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	isfriend: 		产生通知的人是否是自己的好友 1 ：是		
	note: 			评论内容
	dateline: 		通知时间戳
	idtype: 		帖子的类型，如：blogid
	sid: 			帖子的id

	以下参数暂时不用管
	uid: 接收通知人的uid
	type: 通知类型
	
<h3>1．14、	</h3><h3>个人设置读取接口</h3>  
【参数】  
>  

	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/cp.php?ac=profile  
【返回值】  
>  
	
	uid: 			用户uid
	username: 		用户名
	name: 			用户昵称
	realname		真实姓名
	avatar: 		用户头像
	verify_type:	认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	mobile: 		手机号
	verifystatus: 	认证状态：0 未认证；1等待审核；2通过审核	
	verify_address:	认证地址
	sex			 	性别
	marry			婚姻状态
	qq 				qq
	birthcity 		出生省份
	birthprovince 	出生城市
	birth 			生日
	roomid			房屋id
	xiaoquname: 	小区名
	pic_url: 		小区图片
	qiname: 		期
	dongname: 		栋
	cengname: 		层
	roomname: 		室
	privacy：隐私【数组】
			birthcity	家乡隐私 0：全用户可见 3: 仅自己可见
			birth		生日隐私 0：全用户可见 3: 仅自己可见
			qq			qq隐私 0：全用户可见 3: 仅自己可见
			marry		婚姻状态隐私 0：全用户可见 3: 仅自己可见
			mobile		手机隐私 0：全用户可见 3: 仅自己可见
			sex			性别隐私 0：全用户可见 3: 仅自己可见
	
<h3>1．15、	</h3><h3>好友列表接口</h3>  
【参数】  
>  

	group:  分组id 0：全部邻居，1：商家，2：公共服务，3：好友
	page:	当前页【默认1】
	perpage:每页数量【默认10】
	m_auth:	API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=friend  
【返回值】  
>  
	
	uid:      		用户uid
	username: 		用户名
	name:     		用户实名
	avatar:   		用户头像
	verify_type:	认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	note:     		好友备注
	mobile:			手机号 
	ismember:		是否已经关注 1是 0否 
	
<h3>1．16、	</h3><h3>好友分组接口</h3>  
【参数】  
>  

	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

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

	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=request  
【返回值】  
>  
	
	uid: 			用户uid
	username: 		用户名
	avatar: 		用户头像
	name: 			用户实名
	verifystatus: 	认证状态：0 未认证；1等待审核；2通过审核
	verify_type:	认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
	dateline: 		申请时间戳
	
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
	
<h3>1．18、	</h3><h3>赞列表接口</h3>  
【参数】  
>  

	id:			被赞的id
	idtype:		被赞的idtype
	page:		当前页
	perpage:	每页数量
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/do.php?ac=showgood&op=toplist   
【返回值】  
>  
	isshowgood:		  是否已经赞过（是：1，否：0）
	isShowGood: 	  和isshowgood一样，是错误拼写。以后会去除
	showgoods【数组】
		uid: 		  用户uid
		username: 	  用户名
		name:         用户实名
		verify_type:  认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务
		avatar: 	  用户头像 

<h3>1．19、	</h3><h3>推荐好友接口</h3>  
【参数】  
>  

	xiaoquid:	小区的id
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=friend&view=recommend   
【返回值】  
>  
	
	data【数组】
		uid: 		  用户uid  
		username: 	  用户名  
		name:         用户实名  
		verify_type:  认证类型：0、没认证；1、人肉认证；2、住户认证；3、商家认证；4、公共服务  
		avatar: 	  用户头像
		mobile:		  手机号
		ismember:	  是否关注 1是 0否

<h3>1．20、	</h3><h3>获取小区物业分布信息（期、栋、层、房号）接口</h3>  
【参数】  
>  

	xiaoquid:	小区的id
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/do.php?ac=xiaoqustru  
【返回值】  
>  
	
	data【数组】
		qilist:
			qiid		期id			
			qiname		期数名称
			xiaoquid	所属小区
		donglist:
			dongid		栋id
			dongname	栋名称
			qiid		所属期数
		cenglist:
			cengid		层id
			cengname	层名称
			dongid		所属栋
		roomlist:
			roomid		房间id
			roomname	房间名称			
			cengid		所属层

<h3>1．21、	</h3><h3>便民列表接口</h3>  
【参数】  
>  

	xiaoquid:	小区的id【默认是自己小区的id】
	page		当前页【默认1】
	perpage		每页数量【默认10】
	m_auth:		可选。API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=telephone  
【返回值】  
>  
	
	data
		title 		电话名称
		image 		图片
		phone		电话号码

<h3>1．22、	</h3><h3>未处理消息数量接口</h3>  
【参数】  
>  
	
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=allnotenum  
【返回值】  
>  
	
	data
		allnotenum		未处理消息数量
	
<h3>1．23、	</h3><h3>小区周边商家接口</h3>  
【参数】  
>  
	xiaoquid	小区id 
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=adjacent  
【返回值】  
>  
	
	data
		uid: 			商家id
		realname: 		商家真实名字
		name: 			商家昵称
		mobile: 		商家电话
		verify_address: 商家认证地址
		verify_type: 	商家认证 3 
		longitude: 		经度
		latitude:		维度
		note:  			备注
		avatar:			头像

<h3>1．24、	</h3><h3>查询该月份是否已经发布账单接口</h3>  
【参数】  
>  
	year:		年
	month:		月
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/dapi/space.php?do=fee&op=ismonth  
【返回值】  
>  
	data
		set:	该月是否已经发布账单（是：1,；否：0）

<h3>1．25、	</h3><h3>查询该月份该房间是否已经发布账单接口</h3>  
【参数】  
>  
	year:		年
	month:		月
	roomid:		房间ID
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/dapi/space.php?do=fee&op=isfee  
【返回值】  
>  
	data
		set:	该月是否已经发布账单（是：1,；否：0）

<h3>1．26.01、	</h3><h3>获得房间ID接口</h3>  
【参数】  
>  
	qiname:		期
	dongname:	栋
	roomname:	房间
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/dapi/space.php?do=fee&op=roomid  
【返回值】  
>  
	data
		roomid:	房间ID	


<h3>1．26.02、	</h3><h3>通过地址获得房间ID接口</h3>  
【参数】  
>  
	address:		地址
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/dapi/space.php?do=fee&op=getroomid  
【返回值】  
>  
	data
		roomid:	房间ID	


<h3>1．26.03、	</h3><h3>获得所有房间ID接口</h3>  
【参数】  
>  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/dapi/space.php?do=fee&op=allroomids  
【返回值】  
>  
	data
		roomids:	
			i:房间id
			a:地址


<h3>1．27、	</h3><h3>搜索小区接口</h3>  
【参数】  
>

	keyword:	关键字
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/do.php?ac=xiaoqu&op=search  
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


<h3>1．28、	</h3><h3>未读通知数接口</h3>  
【参数】  
>  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=notice&op=count  
【返回值】  
>  
	
	data
		new: 			未读通知数	

<h3>1.29、<h3>一个圈子信息的接口</h3>  
【参数】  
>

	xiaoquid: 	小区id
	tagid:		圈子id
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/space.php?do=mtag&op=info  
【返回值】  
> 
	
		tagid: 圈子id
		tagname: 圈子名
		membernum: 成员数		
		talknum: 圈子吐槽数
		topimages: 图片数组
		close: 圈子开启状态：0 开启 1 关闭
		grade: 允许参与的用户组	
		pic:圈子主题图片
		ismember:是否已经加入

		以下参数暂时不用管
		postnum: 0
		uid: 1
		username: admin		
		fieldid: 1
		xiaoquid: 1	
		threadnum: 帖子数			
		announcement: 没公告……不知道说啥
		closeapply: 0
		joinperm: 0
		viewperm: 0
		threadperm: 0
		postperm: 0
		recommend: 0
		moderator: 	
		title: 其他	




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
	avatar				新浪微博的头像(如果有传这个参数，会更新用户头像)
	
	腾讯微博登陆 
	logintype:			qq  		
	name:				腾讯微博的昵称 
	qq_openid			腾讯微博的id  
	qq_token			腾讯微博token 
	avatar				腾讯微博的头像(如果有传这个参数，会更新用户头像)
	
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
>

	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/do.php?ac=logout  
【返回值】  
>   

		data
			return:  1  
			
<h3>2.7、</h3><h3>赞接口</h3>  
【参数】【GET方式】
>  

	id:			被赞的id
	idtype: 	被赞的idtype
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/do.php?ac=showgood&op=make    
【返回值】  
>   

		data
			result:  1: 已赞 -1: 取消赞  
		
		msgkey：		信息提示码
		msg：			返回的提示信息
		error:			返回的错误的状态, 0无错误，1出错
	
<h3>2.8、	</h3><h3>修改头像接口</h3>  
【参数】  
修改头像：  
>  
	
	Filedata:			文件上传变量
	avatarsubmit:		提交表单用的验证，设为1即可  
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
修改头像：网站域名/dapi/cp.php?ac=avatar  
【返回值】  
>  
	
	data:
		reward:
			credit:		返回的积分
			
<h3>2.9、	</h3><h3>修改昵称接口</h3>  
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
	

<h3>2.10、	</h3><h3>申请成为好友接口</h3>  
【参数】  
>  

	applyuid:		对方的uid；批量申请时，多个uid用|连接，如：1|2|3 
	note:			申请时的附带信息
	addsubmit:		提交申请表单用的验证，设为1即可  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
申请成为好友接口：
网站域名/dapi/cp.php?ac=friend&op=add  

批量申请成为好友接口：
网站域名/dapi/cp.php?ac=friendmul&op=add  

【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错 
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  	
	
<h3>2.11、	</h3><h3>同意成为好友接口</h3>  
【参数】  
>  
	
	applyuid:		申请人的uid
	gid:			分组id
	agreesubmit：	同意申请，设为1即可  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=add  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错	
	
	
<h3>2.12、	</h3><h3>发私信接口</h3>  
【参数】  
>  
	
	touid		对方的uid
	plid		对话列表的id
	message		消息内容
	pmsubmit	提交信息的表单验证，设为1即可  
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=pm&op=send  
【返回值】  
>  
	
	msgkey：			信息提示码
	msg：				返回的提示信息
	error:				返回的错误的状态, 0无错误，1出错
	
	
<h3>2.13、	</h3><h3>发表/转发吐槽接口</h3>  
【参数】  
>  
	
	title		吐槽标题(可选)
	message		吐槽内容
	classid		吐槽分类 调用 <1.5、获得分类接口> 进行选择
	longitude	经度
	latitude	维度
	location	发布地址
	from		发布来源 如：iphone/ipad/android
	picids		图片ids, 多个用|连接, 调用 <2.14 上传照片接口> 得到
	
	转发时需要提供：
	message			转发时填的内容
	forward_id		原吐槽id
	forward_idtype	吐槽的idtype，值为：talkid
	
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=talk&op=addtalk   
【返回值】  
>  
	
	msgkey：			信息提示码
	msg：				返回的提示信息
	error:				返回的错误的状态, 0无错误，1出错	


<h3>2.14、	</h3><h3>上传照片接口</h3>  
【参数】  
>  
	
	Filedata	文件上传变量
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=upload&op=uploadphoto    
【返回值】  
>  
	data:
		picid:			图片id
		thumbpath：		缩略图地址
		picurl：		图片地址
	msgkey：			信息提示码
	msg：				返回的提示信息
	error:				返回的错误的状态, 0无错误，1出错	
	

<h3>2.15、	</h3><h3>设置吐槽分类接口</h3>  
【参数】  
>  
	
	talkid		吐槽id
	classid		分类id
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/cp.php?ac=talk&op=setclassid        
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错		

<h3>2.16、	</h3><h3>申请加入圈子接口</h3>  
【参数】  
>  
	
	tagid		圈子id, 批量加入用 | 连接, 如：1|2|3
	joinsubmit 	1
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=mtag&op=join        
【返回值】  
>  
	data:
		success:		1:直接加入成功；2:需要管理员审核；3:是该圈子不允许加入
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错	

<h3>2.17、	</h3><h3>退出圈子接口</h3>  
【参数】  
>  
	
	tagid		圈子id
	outsubmit 	1
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=mtag&op=out        
【返回值】  
>  
	data:
		success:		退出圈子成功为1，否则为0
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错	

<h3>2.18、	</h3><h3>发表圈子吐槽接口</h3>  
【参数】  
>  
	
	tagid			圈子id
	title			吐槽标题
	message			吐槽内容
	from		发布来源 如：iphone/ipad/android
	picids		图片ids, 多个用|连接, 调用 <2.14 上传照片接口> 得到 
	
	转发时需要提供：
	message			转发时填的内容
	forward_id		原吐槽id 
	forward_idtype	吐槽的idtype，值为：mtalkid 
	
	addsubmit 		1
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=mtag        
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错	
	
<h3>2.19.00、	</h3><h3>发表评论接口</h3>  
【参数】  
>  
	
	id				被评论的帖子id
	idtype			被评论的帖子类型, (talkid, blogid等)
	message			评论内容
	commentsubmit 	1
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=comment         
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错	


<h3>2.19.01、	</h3><h3>回复评论接口</h3>  
【参数】  
>  
	
	id:				被评论的帖子id
	cid:			被回复的评论的cid
	idtype:			被评论的帖子类型, (talkid, blogid等)
	message			评论内容
	commentsubmit 	1
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=comment         
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错	


<h3>2.19.02、	</h3><h3>删除评论接口</h3>  
【参数】  
>  
	
	cid:				被删除评论的cid
	deletesubmit :		1
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=comment&op=delete         
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错	



<h3>2.20、	</h3><h3>个人基本设置保存接口</h3>  
【参数】  
>  
	
	name				昵称
	marry				婚恋状态 0：未设置 1：单身 2：已婚 3：恋爱 	
	sex					性别 1 男 2 女	
	birthyear			出生年
	birthmonth			出生月
	birthday			出生日	
	birthprovince		出生省份
	birthcity			出生城市
	qq					qq	
	note				个人简介
	mobile				手机
	verify_address		认证地址
	
	隐私保护: 	
	friend[birth]		生日隐私 0:全用户可见 3:仅自己可见
	friend[marry]		婚恋状态隐私 0:全用户可见 3:仅自己可见
	friend[sex]			性别隐私 0:全用户可见 3:仅自己可见
	friend[birthcity]	出生地隐私 0:全用户可见 3:仅自己可见		
	friend[qq]			qq隐私 0:全用户可见 3:仅自己可见
	friend[mobile]		手机隐私 0:全用户可见 3:仅自己可见
	
	profilesubmit 		1
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=profile&op=base         
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错			

<h3>2.21、	</h3><h3>个人认证信息保存接口</h3>  
【参数】  
>  
	
	realname			实名	
	mobile				手机号
	roomid				房间号
	xiaoquid			小区id
	profilesubmit 		1
	m_auth:				API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=profile&op=verify         
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错		
	
<h3>2.22、	</h3><h3>取消好友关注接口</h3>  
【参数】  
>  
	
	applyuid:		好友的uid
	friendsubmit	设为1即可  
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
	
【调用方式】  
网站域名/dapi/cp.php?ac=friend&op=ignore  
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错	
	
<h3>2.23、	</h3><h3>修改密码接口</h3>  
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
	

<h3>2.24、	</h3><h3>提交账单接口</h3>  
【参数】  
>

	year：			年
	month：			月
	bill_title		账单标题（非必填）
	bill_message	账单说明（非必填）
	roomid			房间ID
	owner			户主名称
	mobile 			户主手机
	fee_key[]
	fee_timestart[]
	fee_timeend[]
	fee_money[]
	feesubmit		提交信息的表单验证，设为1即可
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/dapi/cp.php?ac=fee&op=add
【返回值】  
>  
	
	msgkey：			信息提示码  
	msg：				返回的提示信息  
	error:				返回的错误的状态, 0无错误，1出错  		
	

<h3>2.25、	</h3><h3>注册时更新小区id接口</h3>  
【参数】  
>

	xiaoquid:	选中小区的xiaoquid
	uid:		注册后，返回的uid
	m_auth:			API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  
【调用方式】  
网站域名/dapi/do.php?ac=register&op=updateid
【返回值】  
>  
	
	msgkey：		信息提示码
	msg：			返回的提示信息
	error:			返回的错误的状态, 0无错误，1出错
	data:
		success:	成功：1  		

<h3>2.26、	</h3><h3>设置主题图片接口</h3>  
【参数】  
>  
	
	picid		图片ids, 多个用|连接, 调用 <2.14 上传照片接口> 得到
	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名/dapi/cp.php?ac=profile&op=theme   
【返回值】  
>  
	
	msgkey：			信息提示码
	msg：				返回的提示信息
	error:				返回的错误的状态, 0无错误，1出错	


<h3>2.27、	</h3><h3>发布商品接口</h3>  
【参数】  
>  
	goodssubmit:	设置为1
	subject：		标题
	message:		内容
	oldprice:		原价
	curprice:		优惠价
	payment：		支付方式（0：货到付款，1：在线付款）
	password：		微信端使用，用于直接微信上查看购买者
	friend：		0：全部小区可见；1：粉丝可见；5：本小区可见；6：指定小区可见；7：指定地区可见

	m_auth:		API密钥, 由登录后返回的，客户端需要存储,每次调用接口需要使用此参数发到服务器  

【调用方式】  
网站域名dapi/cp.php?ac=goods&op=edit   
【返回值】  
>  
	
	msgkey：			信息提示码
	msg：				返回的提示信息
	error:				返回的错误的状态, 0无错误，1出错	