var melogo=localStorage.getItem("melogo");
var ssid=localStorage.getItem("ssid");
var shoplogo=localStorage.getItem("shoplogo");
console.log(melogo);
if(melogo==null){
	melogo="images/3.png";
	
}else{
	
	melogo=localStorage.getItem("melogo");
}
if(shoplogo!=""){
	shoplogo=localStorage.getItem("shoplogo");
}else{
	shoplogo="images/3.png";
}

var username=localStorage.getItem("username");
//if(username==){
//	
//}

function login(){
	var username=localStorage.getItem("username");
	var pp=localStorage.getItem("pp");
	var options = { 
		apiUrl: WebIM.config.apiURL,
		user: username,
		pwd: pp,
		appKey: WebIM.config.appkey
	};
	conn.open(options);
	console.log(options);
}
function doSign(values,data){
    values.sort();
    var str="";
    for(var i in values) {
	   	str+=values[i]+'='+data[values[i]] +'&';       
    }
   str = str.substr(0,str.length-1);
   var key ="idf5nsi5t0qbemwo12hztbftm53tbv6pht";
   var value="idf5nsi5t0qbemwo124213198as";
   var str1 = value+str+'&key='+key+value;
   var sign = (md5(str1)).toUpperCase();
   return sign;
}

function aa(){
	var keys ="idf5nsi5t0qbemwo12hztbftm53tbv6pht";
	var link_url="http://qcap.hangtuosoft.com/index.php?g=app&m=index&a=index&op=";
	var user_id=localStorage.getItem("user_id1");
	var timestamp1 = Date.parse(new Date());
		var values1=["user_id","timestamp"];
		var data1={"user_id":user_id,"timestamp":timestamp1};
		var sign1 = doSign(values1,data1);
		var keys="idf5nsi5t0qbemwo12hztbftm53tbv6pht";
	console.log(user_id);
		console.log(link_url);
		console.log(sign1);
		console.log(timestamp1);
		console.log(keys);
		$.ajax({
			type:"post",
			url: link_url+"updateHxstatus",
			dataType: "json",
			data: {"user_id":user_id,"key":keys,"timestamp":timestamp1,"sign":sign1},
			success: function(data) {
				if(data.status == 1){
					console.log(data);
				}else{
				    $.toast(data.data, "text");
				}
			},
			error:function(){
			 }
		})
}
function register(){
	// 签名
    var nice_name=localStorage.getItem("nice_name");
	var user_name=localStorage.getItem("user_name");
	var user_pwd=localStorage.getItem("user_pwd");

	var options = { 
    username: user_name,
    password: user_pwd,
    nickname: nice_name,
    appKey: WebIM.config.appkey,
    success: function (result) { 
    	console.log(JSON.stringify(result))
    	aa();
//  	alert("注册成功");
    },
    error: function (e){
    	console.log(JSON.stringify(e))
    	console.log(nice_name);
    	console.log(user_name);
    	console.log(user_pwd);
//  	alert("注册失败");
    },
    apiUrl: WebIM.config.apiURL
  }; 
  conn.registerUser(options);
  console.log(options);
}

var conn = {};
		conn = new WebIM.connection({
			isMultiLoginSessions: WebIM.config.isMultiLoginSessions,
			https: typeof WebIM.config.https === 'boolean' ? WebIM.config.https : location.protocol === 'https:',
			url: WebIM.config.xmppURL,
			isAutoLogin: true,
			heartBeatWait: WebIM.config.heartBeatWait,
			autoReconnectNumMax: WebIM.config.autoReconnectNumMax,
			autoReconnectInterval: WebIM.config.autoReconnectInterval,
			isMultiLoginSessions:true
		});

		// listern，添加回调函数
		conn.listen({
			onOpened: function(message) { //连接成功回调，连接成功后才可以发送消息
				//如果isAutoLogin设置为false，那么必须手动设置上线，否则无法收消息
				// 手动上线指的是调用conn.setPresence(); 在本例中，conn初始化时已将isAutoLogin设置为true
				// 所以无需调用conn.setPresence();
				console.log("opened");
//				handleOpen(conn);
				
				//				alert("连接成功");

			},
			onTextMessage: function(message) {
				// 在此接收和处理消息，根据message.type区分消息来源，私聊或群组或聊天室
				//	console.log(message.type);
				console.log(message);
				console.log('Text');

				$('<div class="webim-msg-container rel"><div data-reactroot="" class="rel left"><div class="webim-avatar-icon left small"><img class="w100" src="'+shoplogo+'" style="border-radius:50%"></div><div class="clearfix fl"><div class="webim-msg-value"><span class="webim-msg-icon font">H</span><pre>' + message.data + '</pre></div><div class="webim-msg-error hide"><span class="webim-file-icon font smaller red">k</span></div></div></div></div>').appendTo($(".webim-chatwindow-msg"))

			}, //收到文本消息
			onEmojiMessage: function(message) {
				// 当为WebIM添加了Emoji属性后，若发送的消息含WebIM.Emoji里特定的字符串，connection就会自动将
				// 这些字符串和其它文字按顺序组合成一个数组，每一个数组元素的结构为{type: 'emoji(或者txt)', data:''}
				// 当type='emoji'时，data表示表情图像的路径，当type='txt'时，data表示文本消息
				console.log('Emoji');
				console.log(message);
				var data = message.data;
				var arr = [];
				for(var i = 0, l = data.length; i < l; i++) {
					console.log(data[i]);
					arr.push(data[i]);
				}
				console.log(arr);
				var a = '';
				$.each(arr, function(i, v) {
					if(v.type == "emoji") {
						a += '<img src="' + v.data + '"/>'
					} else if(v.type == "txt") {
						a += '<span>' + v.data + '</span>'
					}
				});
				$('<div class="webim-msg-container rel"><div data-reactroot="" class="rel left"><div class="webim-avatar-icon left small"><img class="w100" src="'+shoplogo+'" style="border-radius:50%"></div><div class="clearfix fl"><div class="webim-msg-value"><span class="webim-msg-icon font">H</span><pre>' + a + '</pre></div><div class="webim-msg-error hide"><span class="webim-file-icon font smaller red">k</span></div></div></div></div>').appendTo($(".webim-chatwindow-msg"))
			}, //收到表情消息
			onPictureMessage: function(message) {
				console.log('Picture');

				var options = {
					url: message.url
				};
				$('<div class="webim-msg-container rel"><div data-reactroot="" class="rel left"><div class="webim-avatar-icon left small"><img class="w100" src="'+shoplogo+'" style="border-radius:50%"></div><div class="clearfix fl"><div class="webim-msg-value"><span class="webim-msg-icon font">H</span><pre><img class="img1" src="' + options.url + '"></pre></div><div class="webim-msg-error hide"><span class="webim-file-icon font smaller red">k</span></div></div></div></div>').appendTo($(".webim-chatwindow-msg"))
				
				options.onFileDownloadComplete = function() {
					// 图片下载成功
					console.log('Image download complete!');
				};
				options.onFileDownloadError = function() {
					// 图片下载失败
					console.log('Image download failed!');
				};
				WebIM.utils.download.call(conn, options); // 意义待查

			}, //收到图片消息
			onCmdMessage: function(message) {
				console.log('CMD');
			}, //收到命令消息
			onAudioMessage: function(message) {
				console.log("Audio");
			}, //收到音频消息
			onLocationMessage: function(message) {
				console.log("Location");
			}, //收到位置消息
			onFileMessage: function(message) {
				console.log("File");
				console.log(message);
				$('<div class="webim-msg-container rel"><div data-reactroot="" class="rel left"><div class="webim-avatar-icon left small"><img class="w100" src="'+shoplogo+'" style="border-radius:50%"></div><p class="left"></p><div class="clearfix" style="min-width: 350px;"><div class="webim-msg-value" style="min-width: 200px;"><span class="webim-msg-icon font">H</span><div><p class="webim-msg-header">文件</p><div id="file_'+message.id+'"><span class="webim-msg-header-icon font small">S</span><span class="webim-msg-name">'+message.filename+'</span><span class="webim-msg-fileSize"></span><a target="_blank" href="'+message.url+'">点击下载</a></div></div></div><div class="webim-msg-error hide"><span class="webim-file-icon font smaller red" title="">k</span></div></div></div></div>').appendTo($(".webim-chatwindow-msg"))
				
			}, //收到文件消息
			onVideoMessage: function(message) {
				var node = document.getElementById('privateVideo');
				var option = {
					url: message.url,
					headers: {
						'Accept': 'audio/mp4'
					},
					onFileDownloadComplete: function(response) {
						var objectURL = WebIM.utils.parseDownloadResponse.call(conn, response);
						node.src = objectURL;
					},
					onFileDownloadError: function() {
						console.log('File down load error.')
					}
				};
				WebIM.utils.download.call(conn, option);
			}, //收到视频消息
			onPresence: function(message) {
				switch(message.type) {
					case 'subscribe': // 对方请求添加好友
						// 同意对方添加好友
						document.getElementById('agreeFriends').onclick = function(message) {
							conn.subscribed({
								to: 'asdfghj',
								message: "[resp:true]"
							});
							// 需要反向添加对方好友
							conn.subscribe({
								to: message.from,
								message: "[resp:true]"
							});
						};
						// 拒绝对方添加好友
						document.getElementById('rejectFriends').onclick = function(message) {
							conn.unsubscribed({
								to: message.from,
								message: "rejectAddFriend" // 拒绝添加好友回复信息
							});
						};

						break;
					case 'subscribed': // 对方同意添加好友，已方同意添加好友
						break;
					case 'unsubscribe': // 对方删除好友
						break;
					case 'unsubscribed': // 被拒绝添加好友，或被对方删除好友成功
						break;
					case 'joinChatRoomSuccess': // 成功加入聊天室
						console.log('join chat room success');
						break;
					case 'joinChatRoomFaild': // 加入聊天室失败
						console.log('join chat room faild');
						break;
					case 'joinPublicGroupSuccess': // 意义待查
						console.log('join public group success', message.from);
						break;
				}
			}, //收到联系人订阅请求（加好友）、处理群组、聊天室被踢解散等消息
			onRoster: function(message) {
				console.log('Roster');

			}, //处理好友申请
			onInviteMessage: function(message) {
				console.log('Invite');
			}, //处理群组邀请
			onOnline: function() {
				console.log('onLine');
			}, //本机网络连接成功
			onOffline: function() {
				console.log('offline');
			}, //本机网络掉线
			onError: function(message) {
				console.log('Error');
				console.log(message);

			}, //失败回调
			onBlacklistUpdate: function(list) {
					// 查询黑名单，将好友拉黑，将好友从黑名单移除都会回调这个函数，list则是黑名单现有的所有好友信息
					console.log(list);
				} // 黑名单变动
		});
		//连接成功时回调方法
		var handleOpen = function(conn) {
			//从连接中获取到当前的登录人注册帐号名
			//  curUserId = conn.context.userId;
			//启动心跳
			if(conn.isOpened()) {
				conn.heartBeat(false);
			}
			conn.setPresence(); //设置上线
			window.location.href="index.html";

		};

		WebIM.Emoji = {
			path: 'css/demo/images/faces/' /*表情包路径*/ ,
			map: {
				'[):]': 'ee_1.png',
				'[:D]': 'ee_2.png',
				'[;)]': 'ee_3.png',
				'[:-o]': 'ee_4.png',
				'[:p]': 'ee_5.png',
				'[(H)]': 'ee_6.png',
				'[:@]': 'ee_7.png',
				'[:s]': 'ee_8.png',
				'[:$]': 'ee_9.png',
				'[:(]': 'ee_10.png',
				"[:'(]": 'ee_11.png',
				'[:|]': 'ee_12.png',
				'[(a)]': 'ee_13.png',
				'[8o|]': 'ee_14.png',
				'[8-|]': 'ee_15.png',
				'[+o(]': 'ee_16.png',
				'[<o)]': 'ee_17.png',
				'[|-)]': 'ee_18.png',
				'[*-)]': 'ee_19.png',
				'[:-#]': 'ee_20.png',
				"[:-*]": 'ee_21.png',
				'[^o)]': 'ee_22.png',
				'[8-)]': 'ee_23.png',
				'[(|)]': 'ee_25.png',
				'[(S)]': 'ee_26.png',
				'[(*)]': 'ee_27.png',
				'[(#)]': 'ee_28.png',
				'[(R)]': 'ee_29.png',
				'[({)]': 'ee_30.png',
				'[(})]': 'ee_31.png',
				"[(k)]": 'ee_32.png',
				'[(F)]': 'ee_33.png',
				'[(W)]': 'ee_34.png',
				'[(D)]': 'ee_35.png'

			}
		};

			//发送消息
		function sendText(toid) {
//			alert(toid);
			textSending = true;
			var msgInput = document.getElementById('talkInputId');
			var msg = msgInput.value;
			if(msg == null || msg.length == 0) {
				return;
			}
			var msgtext = msg.replace(/\n/g, '<br>');
			var id = conn.getUniqueId(); // 生成本地消息id
			var msg = new WebIM.message('txt', id); // 创建文本消息
			msg.set({
				msg: msgtext, // 消息内容
				to: toid, // 接收消息对象（用户id）
				roomType: false,
				success: function(id, serverMsgId) {
					console.log('send private text Success');
				}
			});
			msg.body.chatType = 'singleChat';
			conn.send(msg.body);
			appendMsg(username, toid, msgtext);
			//  turnoffFaces_box();
			msgInput.value = "";
			msgInput.focus();
			setTimeout(function() {
				textSending = false;
			}, 1000);
			$(".cons").keyup();
		};

		function appendMsg(who, contact, message) {
			// 消息体 {isemotion:true;body:[{type:txt,msg:ssss}{type:emotion,msg:imgdata}]}
			var localMsg = null;
			if(typeof message == 'string') {
				localMsg = parseTextMessage(message, WebIM.Emoji.map);
				localMsg = localMsg.body;
			} else {
				localMsg = message.data;
			}
			var a = "";
			for(var i = 0; i < localMsg.length; i++) {
				var msg = localMsg[i];
				var type = msg.type;
				var data = msg.data;
				var src=msg.url;

				console.log(msg);
				console.log(type);
				if(type == "emoji") {
					a += '<img src="' + data + '"/>'

				} else if(type == "File" || type == 'audio' || type == 'video') {
					a += '<img class="img1" src="' + src + '"/>'
				} else {
					a += '<span>' + data + '</span>'
				}

			}
			console.log(a);
			$('<div class="webim-msg-container rel"><div data-reactroot="" class="rel right"><div class="webim-avatar-icon right small"><img class="w100" src="'+melogo+'" style="border-radius:50%"></div><div class="clearfix fl"><div class="webim-msg-value"><span class="webim-msg-icon font">I</span><pre>' + a + '</pre></div><div class="webim-msg-error hide"><span class="webim-file-icon font smaller red">k</span></div></div></div></div>').appendTo($(".webim-chatwindow-msg"))

		}

		function parseTextMessage(message, faces) {
			if(typeof message !== 'string') {
				return;
			}

			if(Object.prototype.toString.call(faces) !== '[object Object]') {
				return {
					isemoji: false,
					body: [{
						type: 'txt',
						data: message
					}]
				};
			}

			var receiveMsg = message;
			var emessage = [];
			var expr = /\[[^[\]]{2,3}\]/mg;
			var emoji = receiveMsg.match(expr);
			console.log(receiveMsg);

			if(!emoji || emoji.length < 1) {
				return {
					isemoji: false,
					body: [{
						type: 'txt',
						data: message
					}]
				};
			}
			var isemoji = false;
			for(var i = 0; i < emoji.length; i++) {
				var tmsg = receiveMsg.substring(0, receiveMsg.indexOf(emoji[i])),
					existEmoji = WebIM.Emoji.map[emoji[i]];

				if(tmsg) {
					emessage.push({
						type: 'txt',
						data: tmsg
					});
				}
				if(!existEmoji) {
					emessage.push({
						type: 'txt',
						data: emoji[i]
					});
					continue;
				}
				var emojiStr = WebIM.Emoji.map ? WebIM.Emoji.path + existEmoji : null;

				if(emojiStr) {
					isemoji = true;
					emessage.push({
						type: 'emoji',
						data: emojiStr
					});
				} else {
					emessage.push({
						type: 'txt',
						data: emoji[i]
					});
				}
				var restMsgIndex = receiveMsg.indexOf(emoji[i]) + emoji[i].length;
				receiveMsg = receiveMsg.substring(restMsgIndex);
			}
			if(receiveMsg) {
				emessage.push({
					type: 'txt',
					data: receiveMsg
				});
			}
			if(isemoji) {
				return {
					isemoji: isemoji,
					body: emessage
				};
			}
			return {
				isemoji: false,
				body: [{
					type: 'txt',
					data: message
				}]
			};
		}
		// 单聊发送图片消息
		function sendPrivateImg(toid) {

			var id = conn.getUniqueId(); // 生成本地消息id
			var msg = new WebIM.message('img', id); // 创建图片消息
			var input = document.getElementById('image'); // 选择图片的input
			var file = WebIM.utils.getFileUrl(input); // 将图片转化为二进制文件
			var allowType = {
				'jpg': true,
				'gif': true,
				'png': true,
				'bmp': true
			};
			if(file.filetype.toLowerCase() in allowType) {
				var option = {
					apiUrl: WebIM.config.apiURL,
					file: file,
					to: toid, // 接收消息对象
					roomType: false,
					chatType: 'singleChat',
					onFileUploadError: function() { // 消息上传失败
						console.log('onFileUploadError');
					},
					onFileUploadComplete: function() { // 消息上传成功
						console.log('onFileUploadComplete');
					},
					success: function() { // 消息发送成功
						console.log('Success');
//						alert(111);
						console.log(file);
						var src=file.url;
						$('<div class="webim-msg-container rel"><div data-reactroot="" class="rel right"><div class="webim-avatar-icon right small"><img class="w100" src="'+melogo+'" style="border-radius:50%"></div><div class="clearfix fl"><div class="webim-msg-value"><span class="webim-msg-icon font">I</span><pre><img class="img1"  src="' + src + '"></pre></div><div class="webim-msg-error hide"><span class="webim-file-icon font smaller red">k</span></div></div></div></div>').appendTo($(".webim-chatwindow-msg"))
						
					},
					flashUpload: WebIM.flashUpload
				};
				msg.set(option);
				conn.send(msg.body);
			}
		};
		// 单聊发送文件消息
		function sendPrivateFile(toid) {
			
			var id = conn.getUniqueId(); // 生成本地消息id
			var msg = new WebIM.message('file', id); // 创建文件消息
			var input = document.getElementById('file'); // 选择文件的input
			var file = WebIM.utils.getFileUrl(input); // 将文件转化为二进制文件
			var allowType = {
				'jpg': true,
				'gif': true,
				'png': true,
				'bmp': true,
				'zip': true,
				'txt': true,
				'doc': true,
				'pdf': true
			};
			if(file.filetype.toLowerCase() in allowType) {
				var option = {
					apiUrl: WebIM.config.apiURL,
					file: file,
					to: toid, // 接收消息对象
					roomType: false,
					chatType: 'singleChat',
					onFileUploadError: function() { // 消息上传失败
						console.log('onFileUploadError');
					},
					onFileUploadComplete: function() { // 消息上传成功
						console.log('onFileUploadComplete');
					},
					success: function() { // 消息发送成功
						console.log('Success');
						console.log(file);
						var filenames=file.filename;
						var filename=filenames.substr(0,10);
						var url=file.url;
						$(".webim-msg-container .right .webim-msg-value").css("margin","6px 4px 0 0");
						$('<div class="webim-msg-container rel"><div data-reactroot="" class="rel right"><div class="webim-avatar-icon right small"><img class="w100" src="'+melogo+'" style="border-radius:50%"></div><p class="right"></p><div class="clearfix" style="min-width: 350px;"><div class="webim-msg-value" style="min-width: 200px;"><span class="webim-msg-icon font">I</span><div><p class="webim-msg-header">文件</p><div id="file_"><span class="webim-msg-header-icon font small">S</span><span class="webim-msg-name">'+filename+'</span><span class="webim-msg-fileSize"></span><a target="_blank" href="'+url+'">点击下载</a></div></div></div><div class="webim-msg-error hide"><span class="webim-file-icon font smaller red" title="">k</span></div></div></div></div>').appendTo($(".webim-chatwindow-msg"))
						
					},
					flashUpload: WebIM.flashUpload
				};
				msg.set(option);
				conn.send(msg.body);
			}
		};