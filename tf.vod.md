# [欢拓点播JS-SDK](http://www.talk-fun.com/) <sup>[v1.0.2](#16-09-2015)</sup>


使用:
------------
- **必须参数 `window.access_token = ${KEY}` 验证KEY**
- **`<script src="//sdk-vod.min.js"></script>` 引入点播SDK包**
- **`var MT = new MT.SDK.main(window.access_token);` 创建SDK对象**


**注意：${KEY} 通过后台接口获取**

事件 & 内置方法:
------------

#####**监听事件 MT.on**
- **`MT.on(@cmd, @callback)`**
	- **参数@cmd: 操作命令**
	- **参数@callback: 回调函数**
<pre>
例：
MT.on("init", function(retval){
	// room init success;
});
</pre>


#####**创建摄像头 MT.camera**
- **`MT.camera(@cameraContainer, @cameraId, @callback)`**
	- **参数@cameraContainer: 摄像头容器**
	- **参数@cameraId: 摄像头id**
	- **参数@callback: 创建完成回调函数**
	- **返回 camera 播放器**
<pre>
例：
MT.camera("cameraContainer", "camerarPlayer", function(camera){
	// cameraPlayer init success;
});
</pre>


#####**创建播放器 MT.mianPlayer**
- **`MT.mianPlayer(@playerContainer, @cameraId, @callback)`**
	- **参数@cameraContainer: 摄像头容器**
	- **参数@cameraId: 摄像头id**
	- **参数@callback: 创建完成回调函数**
	- **返回 player 播放器**
<pre>
例：
MT.mainPlayer("playerContainer", "mainPlayer", function(player){
	// Player init success;
});
</pre>


#####**回放信息 live:info**
- **`live:info`**

	字段					|		类型		|	描述
	---					|		---		|	---
	liveid				| 		string	|	点播id
	title				|		string	|	点播标题
	duration			|		string	|	点播总时间
	views				|		string	|	点播观看次数

<pre>
例：
MT.on('live:info',function(live){
	// liveid: "1259651", title: "20150914开班典礼（侯老师）", duration: "6345", views: "0"
});
</pre>


#####**开始播放 live:start**
- **`live:start`**

<pre>
例：
MT.on('live:start',function(){
	// 开始播放
});
</pre>


#####**暂停播放 live:pause**
- **`live:pause`**

<pre>
例：
MT.on('live:pause',function(){
	// 暂停播放
});
</pre>


#####**停止播放 live:stop**
- **`live:stop`**

<pre>
例：
MT.on('live:stop',function(){
	// 停止播放
});
</pre>


#####**摄像头开启 camera:start**
- **`camera:start`**

<pre>
例：
MT.on('camera:start',function(){
	// 摄像头开启
});
</pre>


#####**摄像头关闭 camera:stop**
- **`camera:stop`**

<pre>
例：
MT.on('camera:stop',function(){
	// 摄像头关闭
});
</pre>


#####**点播视频初始化完成 live:video:loaded**
- **`live:video:loaded`**

<pre>
例：
MT.on('live:video:loaded',function(){
	// 点播视频初始化完成
});
</pre>


#####**聊天分段信息 live:chat:slice**
- **`live:chat:slice`**

	字段				|		类型		|	描述
	---				|		---		|	---
	start			| 		string	|	开始使时间点
	end				|		string	|	结束时间点
	loc				|		string	|	分段xml地址


<pre>
例：
MT.on('live:chat:slice',function(curlist){
	// 返回当前聊天截取信息
});
</pre>


#####**聊天分段详细信息 live:message:append**
- **`live:message:append`**
	- **聊天分段数据，每段默认取200条**

	字段				|		类型		|	描述
	---				|		---		|	---
	message			| 		string	|	聊天信息
	nickname		|		string	|	昵称
	role			|		string	|	角色
	starttime		|		string	|	起始时间点
	timestamp		|		string	|	当前时间戳
	xid				|		string	|	用户xid
	


<pre>
例：
MT.on('live:message:append',function(curlist){
	// 返回一批聊天数据
});
</pre>


#####**问答分段详细信息 live:questions:append**
- **`live:questions:append`**
	- **问答分段数据，每段默认取200条**

	字段				|		类型		|	描述
	---				|		---		|	---
	content			| 		string	|	聊天信息
	nickname		|		string	|	昵称
	role			|		string	|	角色
	starttime		|		string	|	起始时间点
	time			|		string	|	时间
	xid				|		string	|	用户xid
	uid				| 		string	|	用户uid
	liveid			| 		string	|	直播id
	qid				| 		string	|	问答id
	replies			| 		string	|	回复数
	replyId			| 		string	|	回复id
	sn				| 		string	|	问答序号
	


<pre>
例：
MT.on('live:questions:append',function(curlist){
	// 返回一批问答数据
});
</pre>


#####**跳转 MT.seek**
- **`MT.seek(@duration)`**
	- **参数@duration: seek时间点(单位-秒)** 

<pre>
例：
MT.seek(100); // 时间轴从100秒开始播放
</pre>


#####**跳转开始 live:seek:begin**
- **`live:seek:begin`**
	- **返回@duration: seek时间点(单位-秒)** 
<pre>
例：
MT.on("live:seek:begin", function(duration){
	// 返回seek时间点
});
</pre>


#####**跳转完成 live:seek:finish**
- **`live:seek:finish`**
	- **返回@duration: 当前时间点(单位-秒)** 
<pre>
例：
MT.on("live:seek:finish", function(duration){
	// 返回seek时间点
});
</pre>


#####**返回当前时间点 live:duration**
- **`live:seek:finish`**
- `点播播放一旦开始，每隔200毫秒自执行该事件`
	- **返回@currentTime: 当前时间点(单位 秒)** 
	- **返回@duration: 总时长(单位: 秒)** 
	- **返回@currentPercent: 当前播放百分比(单位: 百分比)** 
<pre>
例：
MT.on("live:duration", function(currentTime, duration, currentPercent){
	// 返回seek时间点
});
</pre>



License:
-------
版权所有 @[TalkFun](http://www.talk-fun.com) 解析权归欢拓所有。
