var objMsg = [];//存放所有聊天人和消息的列表
var loginId = "";//存放名字
var chatMessage = "";//存放消息
var meSay = "";//登录人的名字
var youSay = "";//聊天人的名字
var msgList = [];//处理聊天信息
var ueid = "";//聊天人的服务商id
var proAid = "";//点击删除li标签中的div
var lipid = "";//点击切换li
//my pushMessage
var msgStrList = [];
var msgStr = "";
//my partMessage
var msgPartList = [];
var msgPartStr = "";
//my TemMessage
var msgTemList = [];
var msgTemStr = "";

//other pushMessage
var otherPuMsgList = [];
var otherPuMsg = "";
//other partMessage
var otherPaMsgList = [];
var otherPaMsg = "";
//other TemMessage
var otherTeMsgList = [];
var otherTeMsg = "";

var selfTemList = [];
var selfTemStr = "";
//-enterpriseParameter
var curaddress = "";
var curgroupname = "";
var curtel = "";
var curlinkman = "";
var curView = "";
var curNum = "";
var curCateName = "";
var authenticationType = 0;
var nickName = "";
var userOnline = "";
var area = "";
//--projectParameter
var curuserId = "";//发项目的userid
var curNikeName = "";
var curPublish = "";
var curindustry = "";
var curArea = "";
var consultqq = "";
var prostate = 0;//项目状态
var curProDec = "";
var curFilePath = "";
var proType = 0;//类型
var datelimit = 0;
//--pename
var pename = "";
var pelogo = "";
var pnickname = "";
var pisonline = "";
var parea = "";
var peid = "";

var chatData = [];//聊天记录
var loginGroupId = -2;//登录人分类Id
var curGroupId = -1;//发送人分类Id
var pictype = {
    "jpg": true,
    "gif": true,
    "png": true,
    "bmp": true
};
var count = 0;


//初始化连接
$(document).ready(function () {
    if (!Easemob.im.Helper.isCanUploadFileAsync && typeof uploadShim === 'function') {
        swfupload = uploadShim('fileInput');
    }
    handleConfig();

    conn = new Easemob.im.Connection();//创建连接
    //初始化连接
    conn.init({
        https: Easemob.im.config.https,
        url: Easemob.im.config.xmppURL,
        //当连接成功时的回调方法
        onOpened: function () {
            handleOpen(conn);
            console.log("成功");
        },
        //当连接关闭时的回调方法
        onClosed: function () {
            handleClosed();
        },
        //收到文本消息时的回调方法
        onTextMessage: function (message) {
            handleTextMessage(message);
            console.log("收到");
        },
        //收到表情消息时的回调方法
        onEmotionMessage: function (message) {
            handleEmotion(message);
        },
        //收到图片消息时的回调方法
        onPictureMessage: function (message) {
            handlePictureMessage(message);
        },
        //收到音频消息的回调方法
        onAudioMessage: function (message) {
            handleAudioMessage(message);
        },
        //收到位置消息的回调方法
        onLocationMessage: function (message) {
            handleLocationMessage(message);
        },
        //收到文件消息的回调方法
        onFileMessage: function (message) {
            handleFileMessage(message);
        },
        //收到视频消息的回调方法
        onVideoMessage: function (message) {
            handleVideoMessage(message);
        },
        //收到联系人订阅请求的回调方法
        onPresence: function (message) {
            handlePresence(message);
        },
        //收到联系人信息的回调方法
        onRoster: function (message) {
            handleRoster(message);
        },
        //收到群组邀请时的回调方法
        onInviteMessage: function (message) {
            handleInviteMessage(message);
        },
        //异常时的回调方法
        //onError: function (message) {
        //    handleError(message);
        //}
    });
});

////连接成功时回调方法
//var handleOpen = function (conn) {
//  //从连接中获取到当前的登录人注册帐号名
//  curUserId = conn.context.userId;
//  //启动心跳
//  if (conn.isOpened()) {
//      conn.heartBeat(conn);
//  }
//  conn.setPresence();//设置上线
//  if (!Easemob.im.Helper.isCanUploadFileAsync && typeof uploadShim === 'function') {
//      picshim = uploadShim('sendPicInput', 'pic');
//  }
//  window.location.href="index.html";
//};

//连接成功时回调方法
var handleOpen = function (conn) {
   //从连接中获取到当前的登录人注册帐号名
//  curUserId = conn.context.userId;
 //启动心跳
    if (conn.isOpened()) {
        conn.heartBeat(conn);
    }
  conn.setPresence();//设置上线
  window.location.href="index.html";

};


//处理不支持<audio>标签的浏览器，当前只支持MP3
var playAudioShim = function (dom, url, t) {
    var d = $(dom),
        play = d.next(),
        pause = play.next(),
        u = url;
    if (!d.jPlayer) return;
    Easemob.im.Helper.getIEVersion() < 9 && audioDom.push(d);
    d.jPlayer({
        ready: function () {
            $(this).jPlayer("setMedia", {
                mp3: u
            });
        },
        solution: (Easemob.im.Helper.getIEVersion() != 9 ? "html, flash" : "flash"),
        swfPath: "sdk/jplayer",
        supplied: "mp3",
        ended: function () {
            pause.hide();
            play.show();
        }
    });
    play.on('click', function () {
        d.jPlayer('play');
        play.hide();
        pause.show();
    });
    pause.on('click', function () {
        d.jPlayer('pause');
        play.show();
        pause.hide();
    });
};
//处理不支持异步上传的浏览器,使用swfupload作为解决方案
var uploadType = null;
var uploadShim = function (fileInputId) {
    var pageTitle = document.title;
    var uploadBtn = $('#' + fileInputId);
    if (typeof SWFUpload === 'undefined' || uploadBtn.length < 1) return;

    return new SWFUpload({
        file_post_name: 'file'
        , flash_url: "sdk/swfupload/swfupload.swf"
        , button_placeholder_id: fileInputId
        , button_width: uploadBtn.width() || 120
        , button_height: uploadBtn.height() || 30
        , button_cursor: SWFUpload.CURSOR.HAND
        , button_text: '点击上传'
        , button_window_mode: SWFUpload.WINDOW_MODE.TRANSPARENT
        , file_size_limit: 10485760
        , file_upload_limit: 0
        , file_queued_handler: function (file) {
            if (this.getStats().files_queued > 1) {
                this.cancelUpload();
            }
            var checkType = uploadType === 'audio' ? audtype : pictype;
            if (!checkType[file.type.slice(1)]) {
                conn.onError({
                    type: EASEMOB_IM_UPLOADFILE_ERROR,
                    msg: '不支持此文件类型' + file.type
                });
                this.setButtonText('点击上传');
                this.cancelUpload();
            } else if (10485760 < file.size) {
                conn.onError({
                    type: EASEMOB_IM_UPLOADFILE_ERROR,
                    msg: '文件大小超过限制！请上传大小不超过10M的文件'
                });
                this.setButtonText('点击上传');
                this.cancelUpload();
            } else {
                this.setButtonText(file.name);
                flashFilename = file.name;
            }
        }
        , file_dialog_start_handler: function () {
            if (Easemob.im.Helper.getIEVersion() < 10) {
                document.title = pageTitle;
            }
        }
        , upload_error_handler: function (file, code, msg) {
            if (code != SWFUpload.UPLOAD_ERROR.FILE_CANCELLED && code != SWFUpload.UPLOAD_ERROR.UPLOAD_LIMIT_EXCEEDED && code != SWFUpload.UPLOAD_ERROR.FILE_VALIDATION_FAILED) {
                this.uploadOptions.onFileUploadError && this.uploadOptions.onFileUploadError({ type: EASEMOB_IM_UPLOADFILE_ERROR, msg: msg });
            }
        }
        , upload_complete_handler: function () {
            this.setButtonText('点击上传');
        }
        , upload_success_handler: function (file, response) {
            //处理上传成功的回调
            try {
                var res = Easemob.im.Helper.parseUploadResponse(response);

                res = $.parseJSON(res);
                res.filename = file.name;
                this.uploadOptions.onFileUploadComplete && this.uploadOptions.onFileUploadComplete(res);
            } catch (e) {
                conn.onError({
                    type: EASEMOB_IM_UPLOADFILE_ERROR,
                    msg: '上传图片发生错误'
                });
            }
        }
    });
}
//提供上传接口
var flashUpload = function (url, options) {
    if (swfupload.settings.button_text == '点击上传') {
        conn.onError({
            type: EASEMOB_IM_UPLOADFILE_ERROR,
            msg: '请选择文件'
        });
        return;
    }
    swfupload.setUploadURL(url);
    swfupload.uploadOptions = options;
    swfupload.startUpload();
}
var flashPicUpload = function (url, options) {
    flashUpload(picshim, url, options);
};
var getObjectURL = function getObjectURL(file) {
    var url = null;
    if (window.createObjectURL != undefined) { // basic
        url = window.createObjectURL(file);
    } else if (window.URL != undefined) { // mozilla(firefox)
        url = window.URL.createObjectURL(file);
    } else if (window.webkitURL != undefined) { // webkit or chrome
        url = window.webkitURL.createObjectURL(file);
    }
    return url;
};

//判断请求是http还是https
var handleConfig = function () {
    if (Easemob.im.Helper.getIEVersion() < 10) {
        Easemob.im.config.https = location.protocol == 'https:' ? true : false;
        if (!Easemob.im.config.https) {
            if (Easemob.im.config.xmppURL.indexOf('https') == 0) {
                Easemob.im.config.xmppURL = Easemob.im.config.xmppURL.replace(/^https/, 'http');
            }
            if (Easemob.im.config.apiURL.indexOf('https') == 0) {
                Easemob.im.config.apiURL = Easemob.im.config.apiURL.replace(/^https/, 'http');
            }
        } else {
            if (Easemob.im.config.xmppURL.indexOf('http') != -1) {
                Easemob.im.config.xmppURL = Easemob.im.config.xmppURL.replace(/^http/, 'https');
            }
            if (Easemob.im.config.apiURL.indexOf('http') != -1) {
                Easemob.im.config.apiURL = Easemob.im.config.apiURL.replace(/^http/, 'https');
            }
        }
    }
}

//收到文本消息
var handleTextMessage = function (message) {
    var from = message.from;//消息的发送者
    var mestype = message.type;//消息发送的类型是群组消息还是个人消息
    var messageContent = message.data;//文本消息体
    var ext = message.ext;//扩展字段;
    if (ext.hasOwnProperty("projectId") && ext["projectId"] != "") {
            if (ext["projectUserId"] == $("#uid").val()) {
                //我发布的项目
                if (window.location.href.indexOf('TemporaryTalk') >= 0) {
                    document.getElementById('fcount').style.display = "none";
                    //当前页面收到消息给提示 --contactlistUL193
                    var proid = ext["projectId"];
                    var contactULDiv = document.getElementById("contactlistUL" + proid);
                    //隐藏的时候显示 外层
                    if (contactULDiv.style.display == 'none') {
                        selfTemList.push(message.from + "&" + ext["projectId"]);
                        selfTemStr = selfTemList.join(',');
                        document.getElementById('selfStr').value = selfTemStr;
                        var li = $("#" + proid);
                        if (li && li != undefined) {
                            var showMsg = $(li).children(".masege_num");
                            if (showMsg && showMsg.length > 0) {
                                var count = showMsg.text();
                                var myNum = new Number(count);
                                myNum++;
                                showMsg.text(myNum);
                            } else {
                                $("#" + proid).append('<div class="masege_num">1</div>');
                            }
                        }
                    }
                    else {
                        //展开的时候显示 里层
                        appendMsg(from, from, messageContent, ext);//发送
                    }
                }
                else if (window.location.href.indexOf('PushProject') >= 0) {
                    //1.存放消息相关信息
                    msgTemList.push(message.from + "&" + ext["projectId"]);
                    msgTemStr = msgTemList.join(',');
                    document.getElementById('TporaryStr').value = msgTemStr;

                    document.getElementById('fcount').style.display = "block";
                }
                else if (window.location.href.indexOf('Participation') >= 0) {
                    //1.存放消息相关信息
                    msgTemList.push(message.from + "&" + ext["projectId"]);
                    msgTemStr = msgTemList.join(',');
                    document.getElementById('TeporStr').value = msgTemStr;

                    document.getElementById('fcount').style.display = "block";
                }
                else {
                    //其他页面我发布的消息
                    otherTeMsgList.push(message.from + "&" + ext["projectId"]);
                    otherTeMsg = otherTeMsgList.join(',');
                    MessageNotice(3);//消息通知
                }
            }
            else {
                //我参与的项目
                if (window.location.href.indexOf('Participation') >= 0) {
                    document.getElementById('ccount').style.display = "none";
                    appendMsg(from, from, messageContent, ext);//发送
                }
                else if (window.location.href.indexOf('PushProject') != -1) {
                    //1.存放消息相关信息
                    msgPartList.push(message.from + "&" + ext["projectId"]);
                    msgPartStr = msgPartList.join(',');
                    document.getElementById('PumsgStr').value = msgPartStr;
                    document.getElementById('ccount').style.display = "block";
                }
                else if (window.location.href.indexOf('TemporaryTalk') != -1) {
                    //1.存放消息相关信息
                    msgPartList.push(message.from + "&" + ext["projectId"]);
                    msgPartStr = msgPartList.join(',');
                    document.getElementById('TparStr').value = msgPartStr;

                    document.getElementById('ccount').style.display = "block";
                }
                else {
                    //其他页面我参与的消息
                    otherPaMsgList.push(message.from + "&" + ext["projectId"]);
                    otherPaMsg = otherPaMsgList.join(',');
                    MessageNotice(2);//消息通知
                }
            }
    } else {
        //临时会话
        if (window.location.href.indexOf('PushProject') >= 0) {
            document.getElementById('lcount').style.display = "none";
            appendMsg(from, from, messageContent, ext);//发送   
        }
        else if (window.location.href.indexOf('Participation') != -1) {
            //1.存放消息相关信息
            msgStrList.push(message.from);
            msgStr = msgStrList.join(',');
            document.getElementById('PamsgStr').value = msgStr;

            document.getElementById('lcount').style.display = "block";
        }
        else if (window.location.href.indexOf('TemporaryTalk') != -1) {
            //1.存放消息相关信息
            msgStrList.push(message.from);
            msgStr = msgStrList.join(',');
            document.getElementById('TemsgStr').value = msgStr;

            document.getElementById('lcount').style.display = "block";
        }
        else {
            //其他页面临时会话
            otherPuMsgList.push(message.from);
            otherPuMsg = otherPuMsgList.join(',');
            MessageNotice(1);//消息通知
        }
    }
};
//收到表情消息
var handleEmotion = function (message) {
    var from = message.from;
    var room = message.to;
    var mestype = message.type;//消息发送的类型是群组消息还是个人消息
    var messageContent = message.data;//文本消息体
    var ext = message.ext;//扩展字段;
    if (ext.hasOwnProperty("projectId") && ext["projectId"] != "") {
        if (ext["projectUserId"] == $("#uid").val()) {
            //我发布的项目
            if (window.location.href.indexOf('TemporaryTalk') >= 0) {
                document.getElementById('fcount').style.display = "none";
                //当前页面收到消息给提示
                var Picproid = ext["projectId"];
                var contactULDiv = document.getElementById("contactlistUL" + Picproid);
                //隐藏的时候显示 外层
                if (contactULDiv.style.display == 'none') {
                    selfTemList.push(message.from + "&" + ext["projectId"]);
                    selfTemStr = selfTemList.join(',');
                    document.getElementById('selfStr').value = selfTemStr;
                    var li = $("#" + Picproid);
                    if (li && li != undefined) {
                        var showMsg = $(li).children(".masege_num");
                        if (showMsg && showMsg.length > 0) {
                            var count = showMsg.text();
                            var myNum = new Number(count);
                            myNum++;
                            showMsg.text(myNum);
                        } else {
                            $("#" + Picproid).append('<div class="masege_num">1</div>');
                        }
                    }
                }
                else {
                    //展开的时候显示 里层
                    appendMsg(from, from, message, ext);//发送
                }
            }
            else if (window.location.href.indexOf('PushProject') != -1) {
                //1.存放消息相关信息
                msgTemList.push(message.from + "&" + ext["projectId"]);
                msgTemStr = msgTemList.join(',');
                document.getElementById('TporaryStr').value = msgTemStr;
                document.getElementById('fcount').style.display = "block";
            }
            else if (window.location.href.indexOf('Participation') != -1) {
                //1.存放消息相关信息
                msgTemList.push(message.from + "&" + ext["projectId"]);
                msgTemStr = msgTemList.join(',');
                document.getElementById('TeporStr').value = msgTemStr;
                document.getElementById('fcount').style.display = "block";
            }
            else {
                //其他页面我发布的消息
                otherTeMsgList.push(message.from + "&" + ext["projectId"]);
                otherTeMsg = otherTeMsgList.join(',');
                MessageNotice(3);//消息通知
            }
        }
        else {
            //我参与的项目
            if (window.location.href.indexOf('Participation') >= 0) {
                document.getElementById('ccount').style.display = "none";
                appendMsg(from, from, message, ext);//发送
            }
            else if (window.location.href.indexOf('PushProject') != -1) {
                //1.存放消息相关信息
                msgPartList.push(message.from + "&" + ext["projectId"]);
                msgPartStr = msgPartList.join(',');
                document.getElementById('PumsgStr').value = msgPartStr;
                document.getElementById('ccount').style.display = "block";
            }
            else if (window.location.href.indexOf('TemporaryTalk') != -1) {
                //1.存放消息相关信息
                msgPartList.push(message.from + "&" + ext["projectId"]);
                msgPartStr = msgPartList.join(',');
                document.getElementById('TparStr').value = msgPartStr;
                document.getElementById('ccount').style.display = "block";
            }
            else {
                //其他页面我参与的消息
                otherPaMsgList.push(message.from + "&" + ext["projectId"]);
                otherPaMsg = otherPaMsgList.join(',');
                MessageNotice(2);//消息通知
            }
        }
    }
    else {
        //临时会话
        if (window.location.href.indexOf('PushProject') >= 0) {
            document.getElementById('lcount').style.display = "none";
            appendMsg(from, from, message, ext);//发送   
        }
        else if (window.location.href.indexOf('Participation') != -1) {
            //1.存放消息相关信息
            msgStrList.push(message.from);
            msgStr = msgStrList.join(',');
            document.getElementById('PamsgStr').value = msgStr;

            document.getElementById('lcount').style.display = "block";
        }
        else if (window.location.href.indexOf('TemporaryTalk') != -1) {
            //1.存放消息相关信息
            msgStrList.push(message.from);
            msgStr = msgStrList.join(',');
            document.getElementById('TemsgStr').value = msgStr;

            document.getElementById('lcount').style.display = "block";
        }
        else {
            //其他页面临时会话
            otherPuMsgList.push(message.from);
            otherPuMsg = otherPuMsgList.join(',');
            MessageNotice(1);//消息通知
        }
    }
};
//收到图片消息
var handlePictureMessage = function (message){
    var filename = message.filename;//文件名称，带文件扩展名
    var from = message.from;//文件的发送者
    var mestype = message.type;//消息发送的类型是群组消息还是个人消息
    var contactDivId = from;
    var options = message;
    var ext = message.ext;
    if (ext.hasOwnProperty("projectId") && ext["projectId"] != "") {
            //我发布的
        if (ext["projectUserId"] == $("#uid").val()) {
                if (window.location.href.indexOf('TemporaryTalk') >= 0) {
                    document.getElementById('fcount').style.display = "none";
                    //当前页面收到消息给提示
                    var Imgproid = ext["projectId"];
                    var contactULDiv = document.getElementById("contactlistUL" + Imgproid);
                    //隐藏的时候显示 外层
                    if (contactULDiv.style.display == 'none') {
                        selfTemList.push(message.from + "&" + ext["projectId"]);
                        selfTemStr = selfTemList.join(',');
                        document.getElementById('selfStr').value = selfTemStr;
                        var li = $("#" + Imgproid);
                        if (li && li != undefined) {
                            var showMsg = $(li).children(".masege_num");
                            if (showMsg && showMsg.length > 0) {
                                var count = showMsg.text();
                                var myNum = new Number(count);
                                myNum++;
                                showMsg.text(myNum);
                            } else {
                                $("#" + Imgproid).append('<div class="masege_num">1</div>');
                            }
                        }
                    }
                    else {
                        //展开的时候显示 里层
                        // 图片消息下载成功后的处理逻辑
                        options.onFileDownloadComplete = function (response, xhr) {
                            var objectURL = Easemob.im.Helper.parseDownloadResponse.call(this, response);
                            img = document.createElement("img");
                            img.onload = function (e) {
                                img.onload = null;
                                window.URL && window.URL.revokeObjectURL && window.URL.revokeObjectURL(img.src);
                            };
                            img.onerror = function () {
                                img.onerror = null;
                                if (typeof FileReader == 'undefined') {
                                    img.alter = "当前浏览器不支持blob方式";
                                    return;
                                }
                                img.onerror = function () {
                                    img.alter = "当前浏览器不支持blob方式";
                                };
                                var reader = new FileReader();
                                reader.onload = function (event) {
                                    img.src = this.result;
                                };
                                reader.readAsDataURL(response);
                            }

                            img.src = objectURL;
                            var pic_real_width = options.width;
                            if (!pic_real_width || pic_real_width == 0) {
                                $("<img/>").attr("src", objectURL).load(function () {
                                    pic_real_width = this.width;
                                    if (pic_real_width > maxWidth) {
                                        img.width = maxWidth;
                                    } else {
                                        img.width = pic_real_width;
                                    }
                                });
                            } else {
                                if (pic_real_width > maxWidth) {
                                    img.width = maxWidth;
                                } else {
                                    img.width = pic_real_width;
                                }
                            }
                            appendMsg(from, contactDivId, {
                                data: [{
                                    type: 'pic',
                                    filename: objectURL,
                                    data: img
                                }]
                            }, ext);//发送
                        };
                    }
                }
                else if (window.location.href.indexOf('PushProject') >= 0) {
                    //1.存放消息相关信息
                    msgTemList.push(message.from + "&" + ext["projectId"]);
                    msgTemStr = msgTemList.join(',');
                    document.getElementById('TporaryStr').value = msgTemStr;
                    document.getElementById('fcount').style.display = "block";
                }
                else if (window.location.href.indexOf('Participation') >= 0) {
                    //1.存放消息相关信息
                    msgTemList.push(message.from + "&" + ext["projectId"]);
                    msgTemStr = msgTemList.join(',');
                    document.getElementById('TeporStr').value = msgTemStr;
                    document.getElementById('fcount').style.display = "block";
                }
                else {
                    //其他页面我发布的消息
                    otherTeMsgList.push(message.from + "&" + ext["projectId"]);
                    otherTeMsg = otherTeMsgList.join(',');
                    MessageNotice(3);//消息通知
                }
            }
            else {
                //我参与的
                if (window.location.href.indexOf('Participation') >= 0) {
                    document.getElementById('ccount').style.display = "none";
                    // 图片消息下载成功后的处理逻辑
                    options.onFileDownloadComplete = function (response, xhr) {
                        var objectURL = Easemob.im.Helper.parseDownloadResponse.call(this, response);
                        img = document.createElement("img");
                        img.onload = function (e) {
                            img.onload = null;
                            window.URL && window.URL.revokeObjectURL && window.URL.revokeObjectURL(img.src);
                        };
                        img.onerror = function () {
                            img.onerror = null;
                            if (typeof FileReader == 'undefined') {
                                img.alter = "当前浏览器不支持blob方式";
                                return;
                            }
                            img.onerror = function () {
                                img.alter = "当前浏览器不支持blob方式";
                            };
                            var reader = new FileReader();
                            reader.onload = function (event) {
                                img.src = this.result;
                            };
                            reader.readAsDataURL(response);
                        }

                        img.src = objectURL;
                        var pic_real_width = options.width;
                        if (!pic_real_width || pic_real_width == 0) {
                            $("<img/>").attr("src", objectURL).load(function () {
                                pic_real_width = this.width;
                                if (pic_real_width > maxWidth) {
                                    img.width = maxWidth;
                                } else {
                                    img.width = pic_real_width;
                                }
                            });
                        } else {
                            if (pic_real_width > maxWidth) {
                                img.width = maxWidth;
                            } else {
                                img.width = pic_real_width;
                            }
                        }
                        appendMsg(from, contactDivId, {
                            data: [{
                                type: 'pic',
                                filename: objectURL,
                                data: img
                            }]
                        }, ext);//发送
                    };
                }
                else if (window.location.href.indexOf('PushProject') != -1) {
                    //1.存放消息相关信息
                    msgPartList.push(message.from + "&" + ext["projectId"]);
                    msgPartStr = msgPartList.join(',');
                    document.getElementById('PumsgStr').value = msgPartStr;
                    document.getElementById('ccount').style.display = "block";
                }
                else if (window.location.href.indexOf('TemporaryTalk') != -1) {
                    //1.存放消息相关信息
                    msgPartList.push(message.from + "&" + ext["projectId"]);
                    msgPartStr = msgPartList.join(',');
                    document.getElementById('TparStr').value = msgPartStr;
                    document.getElementById('ccount').style.display = "block";
                }
                else {
                    //其他页面我参与的消息
                    otherPaMsgList.push(message.from + "&" + ext["projectId"]);
                    otherPaMsg = otherPaMsgList.join(',');
                    MessageNotice(2);//消息通知
                }
            }
    }
    else {
        //临时会话
        if (window.location.href.indexOf('PushProject') >= 0) {
            document.getElementById('lcount').style.display = "none";
            // 图片消息下载成功后的处理逻辑
            options.onFileDownloadComplete = function (response, xhr) {
                var objectURL = Easemob.im.Helper.parseDownloadResponse.call(this, response);
                img = document.createElement("img");
                img.onload = function (e) {
                    img.onload = null;
                    window.URL && window.URL.revokeObjectURL && window.URL.revokeObjectURL(img.src);
                };
                img.onerror = function () {
                    img.onerror = null;
                    if (typeof FileReader == 'undefined') {
                        img.alter = "当前浏览器不支持blob方式";
                        return;
                    }
                    img.onerror = function () {
                        img.alter = "当前浏览器不支持blob方式";
                    };
                    var reader = new FileReader();
                    reader.onload = function (event) {
                        img.src = this.result;
                    };
                    reader.readAsDataURL(response);
                }

                img.src = objectURL;
                var pic_real_width = options.width;
                if (!pic_real_width || pic_real_width == 0) {
                    $("<img/>").attr("src", objectURL).load(function () {
                        pic_real_width = this.width;
                        if (pic_real_width > maxWidth) {
                            img.width = maxWidth;
                        } else {
                            img.width = pic_real_width;
                        }
                    });
                } else {
                    if (pic_real_width > maxWidth) {
                        img.width = maxWidth;
                    } else {
                        img.width = pic_real_width;
                    }
                }
                appendMsg(from, contactDivId, {
                    data: [{
                        type: 'pic',
                        filename: objectURL,
                        data: img
                    }]
                }, ext);//发送
            }; 
        }
        else if (window.location.href.indexOf('Participation') != -1) {
            //1.存放消息相关信息
            msgStrList.push(message.from);
            msgStr = msgStrList.join(',');
            document.getElementById('PamsgStr').value = msgStr;
            document.getElementById('lcount').style.display = "block";
        }
        else if (window.location.href.indexOf('TemporaryTalk') != -1) {
            //1.存放消息相关信息
            msgStrList.push(message.from);
            msgStr = msgStrList.join(',');
            document.getElementById('TemsgStr').value = msgStr;
            document.getElementById('lcount').style.display = "block";
        }
        else {
            //其他页面临时会话
            otherPuMsgList.push(message.from);
            otherPuMsg = otherPuMsgList.join(',');
            MessageNotice(1);//消息通知
        }
    }
    var redownLoadFileNum = 0;
    options.onFileDownloadError = function (e) {
        //下载失败时只重新下载一次
        if (redownLoadFileNum < 1) {
            redownLoadFileNum++;
            options.accessToken = options_c;
            Easemob.im.Helper.download(options);

        } else {
            appendMsg(from, contactDivId, e.msg + ",下载图片" + filename + "失败", "");
            redownLoadFileNum = 0;
        }

    };
    //easemobwebim-sdk包装的下载文件对象的统一处理方法。
    Easemob.im.Helper.download(options);
};


//发送消息
function sendText() {
   textSending = true;
    var msgInput = document.getElementById('talkInputId');
    var msg = msgInput.value;
    if (msg == null || msg.length == 0) {
        return;
    }
    var to = "18991360884";
    if (to == null) {
        return;
    }
    var msgtext = msg.replace(/\n/g, '<br>');

	 var options = {
	        to: to,
	        msg: msg,
	        type: "chat",
	    };
	conn.sendTextMessage(options);
	appendMsg("121218837qq.com", to, msgtext);
    turnoffFaces_box();
    msgInput.value = "";
    msgInput.focus();
    setTimeout(function () {
        textSending = false;
    }, 1000);

};

function appendMsg(who, contact, message) {
	// 消息体 {isemotion:true;body:[{type:txt,msg:ssss}{type:emotion,msg:imgdata}]}
 	var localMsg = null;
    if (typeof message == 'string') {
        localMsg = Easemob.im.Helper.parseTextMessage(message);
        localMsg = localMsg.body;
    } else {
        localMsg = message.data;
    }
	for (var i = 0; i < localMsg.length; i++) {
        var msg = localMsg[i];
        var type = msg.type;
        var data = msg.data;
        var a;
        if (type == "emotion") {
        	a='<img src="'+data+'"/>'

		}else if (type == "pic" || type == 'audio' || type == 'video') {
			a='<img src="'+data+'"/>'
		} else {
			a='<span>'+data+'</span>'
		}
			$('<div class="webim-msg-container rel"><div data-reactroot="" class="rel right"><div class="webim-avatar-icon right small"><img class="w100" src="images/3.png"></div><div class="clearfix fl"><div class="webim-msg-value"><span class="webim-msg-icon font">I</span><pre>'+a+'</pre></div><div class="webim-msg-error hide"><span class="webim-file-icon font smaller red">k</span></div></div></div></div>').appendTo($(".webim-chatwindow-msg"))	
		
	}

}


//发送图片消息
var sendPic = function ()  {
    var to = curChatUserId;
    if (to == null) {
        return;
    }
    var projectId = "";
    if (window.location.href.indexOf('Participation') > 0) {
        projectId = lipid;
    }
    else {
        projectId = $("#thisProId").val();
    }
    getProInfo(projectId);
    getCurEnterprise($("#uid").val());
    var enterpriseName = $("#uname").val();
    var enterpriseLogo = $("#ulogo").val();
    if (enterpriseName == "") {
        enterpriseName = nickName
    }
    else {
        enterpriseName = enterpriseName
    }
    // Easemob.im.Helper.getFileUrl为easemobwebim-sdk获取发送文件对象的方法，fileInputId为 input 标签的id值
    var fileObj = Easemob.im.Helper.getFileUrl('fileInput');
    if (Easemob.im.Helper.isCanUploadFileAsync && (fileObj.url == null || fileObj.url == '')) {
        alert("请先选择图片");
        return;
    }
    var filetype = fileObj.filetype || '';
    var filename = fileObj.filename;
    if (!Easemob.im.Helper.isCanUploadFileAsync || filetype.toLowerCase() in pictype) {
        var opt = {
            type: 'chat',
            fileInputId: 'fileInput',
            filename: flashFilename || filename,
            to: to,
            ext: { enterpriseName: enterpriseName, enterpriseLogo: enterpriseLogo, projectType: "0", enterpriseId: $("#enpid").val(), projectUserId: curuserId, projectId: projectId},
            apiUrl: Easemob.im.config.apiURL,
            onFileUploadError: function (error) {
                var messageContent = (error.msg || '') + ",发送图片文件失败:" + (filename || flashFilename);
                message.alert("图片发送失败,网络异常！");
                //appendMsg(curUserId, to, messageContent);
            },
            onFileUploadComplete: function (data) {
                var file = document.getElementById('fileInput');
                if (Easemob.im.Helper.isCanUploadFileAsync && file && file.files) {
                    var objUrl = getObjectURL(file.files[0]);
                    if (objUrl) {
                        var img = document.createElement("img");
                        img.src = objUrl;
                        img.width = maxWidth;
                    }
                } else {
                    filename = data.filename || '';
                    var img = document.createElement("img");
                    img.src = data.uri + '/' + data.entities[0].uuid;
                    img.width = maxWidth;
                }
                var ext = opt["ext"];
                //判断是我发布
                if (ext["projectUserId"] != 0 && ext["projectUserId"] == $("#uid").val()) {
                    appendMsg(curUserId, to, {
                        data: [{
                            type: 'pic',
                            filename: objUrl,
                            data: img
                        }],
                    }, ext);
                }
                else {
                    appendMsg(curUserId, to, {
                        data: [{
                            type: 'pic',
                            filename: objUrl,
                            data: img
                        }],
                    }, ext);
                }
                //当环信发送图片成功时在去往数据库写数据
                var myfile = $("#fileInput").get(0).files[0];//获取图片
                var fileFrom = new FormData();//存放图片
                //发送人
                var mySpeakerid = "kuaijing" + $("#uid").val();
                //接收人
                var myaudienceid = to;
                fileFrom.append("chatpic", myfile);
                fileFrom.append("ename", enterpriseName);
                fileFrom.append("elogo", enterpriseLogo);
                fileFrom.append("speakerid", mySpeakerid);
                fileFrom.append("audienceid", myaudienceid);
                fileFrom.append("projectid", projectId);
                //上传图片到服务器
                $.ajax({
                    type: "POST",
                    contentType: false, //必须false才会避开jQuery对 formdata 的默认处理 , XMLHttpRequest会对 formdata 进行正确的处理
                    processData: false, //必须false才会自动加上正确的Content-Type 
                    url: '/ProjectFile/UploadChatImg',
                    data: fileFrom,
                    success: function (data) {
                    },
                    error: function (msg) {
                        message.alert("图片上传失败,请重新尝试！");
                    }
                });
            },
            flashUpload: flashPicUpload
        };
        //if (curChatUserId.indexOf(groupFlagMark) >= 0) {
        //    opt.type = groupFlagMark;
        //    opt.to = curRoomId;
        //} else if (curChatUserId.indexOf(chatRoomMark) >= 0) {
        //    opt.type = groupFlagMark;
        //    opt.roomType = chatRoomMark;
        //    opt.to = curChatRoomId;
        //}
        conn.sendPicture(opt);
        return;
    }
    alert("不支持此图片类型" + filetype);
};

//发送音频消息
var handleAudioMessage = function (message) {
    if (document.getElementById('webImContent').style.display == "none") {
        //$("#msg").css("display", "block");
        //$(".chat_content_right_b p").css("margin-left", "33px");
        $("#webim-show").css("background", "url(/Content/img/notice.gif)");
    }
    var filename = message.filename;
    var filetype = message.filetype;
    var from = message.from;
    var mestype = message.type;//消息发送的类型是群组消息还是个人消息
    var ext = message.ext;//扩展字段
    var contactDivId = from;
    if (mestype == groupFlagMark || mestype == chatRoomMark) {
        contactDivId = mestype + message.to;
    }
    var audio = document.createElement("audio");
    audio.controls = "controls";
    audio.innerHTML = "当前浏览器不支持播放此音频:" + filename;
    //audio.src = message.url;
    if (ext.hasOwnProperty("projectType")) {
        if (ext.hasOwnProperty("projectId") && ext.projectType == "0") {
            var proid = ext["projectId"];
            document.getElementById('curproid').value = proid;
            var uid = $("#uid").val();
            $.ajax({
                type: "post",
                url: "/Conslut/IsMyProject",
                data: { "proid": proid },
                dataType: "json",
                async: false,
                success: function (data) {
                    if (data.consult_UserID == $("#uid").val() && $("#contactlistUL li").length == 0) {
                        showCss(data.consult_ProjectDescription);
                        //显示发布修改按钮
                        document.getElementById('proEdit').style.display = "block";
                        document.getElementById('proSend').style.display = "block";
                        document.getElementById('proinfo').style.display = "none";
                    }
                    else {
                        if ($("#contactlistUL li").length == 0) {
                            showCss(data.consult_ProjectDescription);
                        }
                    }
                }
            });
        }
    }
    appendMsg(from, contactDivId, {
        data: [{
            type: 'audio',
            filename: filename || '',
            data: audio,
            audioShim: !window.Audio
        }]
    }, ext);
    var options = message;
    options.onFileDownloadComplete = function (response, xhr) {
        var objectURL = Easemob.im.Helper.parseDownloadResponse.call(this, response);
        if (Easemob.im.Helper.getIEVersion != 9 && window.Audio) {
            audio.onload = function () {
                audio.onload = null;
                window.URL && window.URL.revokeObjectURL && window.URL.revokeObjectURL(audio.src);
            };
            audio.onerror = function () {
                audio.onerror = null;
            };
            audio.src = objectURL;
            return;
        }
    };
    options.onFileDownloadError = function (e) {
        appendMsg(from, contactDivId, e.msg + ",下载音频" + filename + "失败", "");
    };
    options.headers = {
        "Accept": "audio/mp3"
    };
    Easemob.im.Helper.download(options);
};

//返回时间
var getLoacalTimeString = function getLoacalTimeString() {
    var date = new Date();
    var month = date.getMonth() + 1;
    var time = date.getFullYear() + "/" + month + "/" + date.getDate() + " " + date.getHours() + ":" + date.getMinutes() + ":" + date.getSeconds();
    return time;
}

//登陆
function login(user,pass) {
    var user = user;
    curUserId = user;
    var pass = pass;
    if (user == '' || pass == '') {
        alert("请输入用户名和密码");
        return;
    }
    //根据用户名密码登录系统
    conn.open({
        apiUrl: Easemob.im.config.apiURL,
        user: user,
        pwd: pass,
        //连接时提供appkey
        appKey: Easemob.im.config.appkey
    });
};

//导入聊天包
function loadEmotionImg() {
    var sjson = Easemob.im.Helper.EmotionPicData;
    for (var key in sjson) {
        var emotions = $('<img>').attr({
            "id": key,
            "src": sjson[key],
            "style": "cursor:pointer;"
        }).click(function () {
            selectEmotionImg(this);
        });
        $('<li>').append(emotions).appendTo($('#emotionUL'));
    }
}

//选择聊天表情添加到文本框并关闭聊天表情div
function selectEmotionImg(selImg) {
    var txt = document.getElementById("talkInputId");
    txt.value = txt.value + selImg.id;
    txt.focus();
    turnoffFaces_box();
}
//聊天表情导入
function showEmotionDialog() {
    $('#wl_faces_box').css({
        "display": "block"
    });
}
//表情div关闭方法
function turnoffFaces_box() {
    $("#wl_faces_box").fadeOut("fast");
}


//本地上传--然后发送图片消息
function sendPicMessage(id, proid) {
    var to = "kuaijing" + id;
    if (to == null) {
        return;
    }
    getCurEnterprise($("#uid").val());
    var enterpriseName = $("#uname").val();
    var enterpriseLogo = $("#ulogo").val();
    var nikeName = $()
    if (enterpriseName == "") {
        enterpriseName = nickName
    }
    else {
        enterpriseName = enterpriseName
    }
    // Easemob.im.Helper.getFileUrl为easemobwebim-sdk获取发送文件对象的方法，fileInputId为 input 标签的id值
    var fileObj = Easemob.im.Helper.getFileUrl('file');
    if (Easemob.im.Helper.isCanUploadFileAsync && (fileObj.url == null || fileObj.url == '')) {
        alert("请先选择图片");
        return;
    }
    var filetype = fileObj.filetype || '';
    var filename = fileObj.filename;
    if (!Easemob.im.Helper.isCanUploadFileAsync || filetype.toLowerCase() in pictype) {
        var opt = {
            type: 'chat',
            fileInputId: 'file',
            filename: flashFilename || filename,
            to: to,
            ext: { enterpriseName: enterpriseName, enterpriseLogo: enterpriseLogo, projectType: "0", enterpriseId: $("#enpid").val(), projectUserId: id, projectId: proid},
            apiUrl: Easemob.im.config.apiURL,
            onFileUploadError: function (error) {
                var messageContent = (error.msg || '') + ",发送图片文件失败:" + (filename || flashFilename);
                message.alert("图片发送失败,网络异常！");
            },
            onFileUploadComplete: function (data) {
                var file = document.getElementById('file');
                if (Easemob.im.Helper.isCanUploadFileAsync && file && file.files) {
                    var objUrl = getObjectURL(file.files[0]);
                    if (objUrl) {
                        var img = document.createElement("img");
                        img.src = objUrl;
                        img.width = maxWidth;
                    }
                } else {
                    filename = data.filename || '';
                    var img = document.createElement("img");
                    img.src = data.uri + '/' + data.entities[0].uuid;
                    img.width = maxWidth;
                }
                    //当环信发送图片成功时在去往数据库写数据
                    var myfile = $("#file").get(0).files[0];//获取图片
                    var fileFrom = new FormData();//存放图片
                    var enterpriseName = $("#cname").val();
                    var enterpriseLogo = $("#clogo").val();
                    //发送人
                    var mySpeakerid = "kuaijing" + $("#uid").val();
                    //接收人
                    var myaudienceid = "kuaijing" + id;
                    fileFrom.append("chatpic", myfile);
                    fileFrom.append("ename", enterpriseName);
                    fileFrom.append("elogo", enterpriseLogo);
                    fileFrom.append("speakerid", mySpeakerid);
                    fileFrom.append("audienceid", myaudienceid);
                    fileFrom.append("projectid", proid);
                    //上传图片到服务器
                    $.ajax({
                        type: "POST",
                        contentType: false, //必须false才会避开jQuery对 formdata 的默认处理 , XMLHttpRequest会对 formdata 进行正确的处理
                        processData: false, //必须false才会自动加上正确的Content-Type 
                        url: '/ProjectFile/UploadChatImg',
                        data: fileFrom,
                        success: function (data) {
                            if (data != 0) {
                                closeThis();
                                window.location.href = "../Chat/Participation?uid=" + id + "&&pid=" + proid + "";
                            }
                            else {
                                message.alert("图片上传失败,请重新尝试");
                            }
                        },
                        error: function (msg) {
                            message.alert("图片上传失败,请重新尝试！");
                        }
                    });
            },
            flashUpload: flashPicUpload
        };
        conn.sendPicture(opt);
        return;
    }
    alert("不支持此图片类型" + filetype);
}
//查看聊天记录
function chakan() {
    window.open("/usercenter/massage");
}
//消息通知
function MessageNotice(PageFlag) {
    //消息提示1 == 双向消息提示
    var message = {
        time: 0,
        title: document.title,
        timer: null,
        // 显示新消息提示
        show: function () {
            var title = message.title.replace("【　　　】", "").replace("【新消息】", "");
            // 定时器，设置消息切换频率闪烁效果就此产生
            message.timer = setTimeout(function () {
                message.time++;
                message.show();
                if (message.time % 2 == 0) {
                    document.title = "【新消息】" + title
                }

                else {
                    document.title = "【　　　】" + title
                };
            }, 600);
            return [message.timer, message.title];
        },
        // 取消新消息提示
        clear: function () {
            clearTimeout(message.timer);
            document.title = message.title;
        }
    };
    message.show();
    if (window.location.href.indexOf('TemporaryTalk') >= 0 || window.location.href.indexOf('Participation') >= 0 || window.location.href.indexOf('PushProject') >= 0) {
        message.clear();
    }
    //消息提示2 -H5
    if (window.Notification) {
        var chatFlag = true;
        if (window.location.href.indexOf('TemporaryTalk') >= 0 || window.location.href.indexOf('Participation') >= 0 || window.location.href.indexOf('PushProject') >= 0) {
            chatFlag = false;
        }
        var popNotice = function () {
            if (Notification.permission == "granted") {
                var notification = new Notification("尊敬的快竞用户：", {
                    body: '您收到了一条新的消息,点击进行查看>>>',
                    icon: '/Images/Chatlogo.png'
                });

                notification.onclick = function () {
                    if (PageFlag == 1) {
                        window.location.href = '../Chat/PushProject.html?id=' + strEnc(otherPuMsg, "=", "", "");
                    }
                    else if (PageFlag == 2) {
                        window.location.href = '../Chat/Participation.html?id=' + strEnc(otherPaMsg, "=", "", "");
                    }
                    else if (PageFlag == 3) {
                        window.location.href = '../Chat/TemporaryTalk.html?id=' + strEnc(otherTeMsg, "=", "", "");
                    }
                    window.focus();
                    notification.close();
                };
            }
        };

        if (chatFlag) {
            if (Notification.permission == "granted") {
                popNotice();
            } else if (Notification.permission != "denied") {
                Notification.requestPermission(function (permission) {
                    popNotice();
                });
            }
        };
    } else {
        alert('浏览器不支持Notification');
    }
    //消息提示结束
}
//保存案例上传图片 - 聊天
function uploadImg(id,projectid,strUrl) {
    //当环信发送图片成功时在去往数据库写数据
    var myfile = strUrl;//图片地址
    var fileFrom = new FormData();//存放图片
    getCurEnterprise($("#uid").val());
    var enterpriseName = $("#uname").val();
    var enterpriseLogo = $("#ulogo").val();
    var nikeName = $()
    if (enterpriseName == "") {
        enterpriseName = nickName
    }
    else {
        enterpriseName = enterpriseName
    }
    //发送人
    var mySpeakerid = "kuaijing" + $("#uid").val();
    //接收人
    var myaudienceid = "kuaijing" + id;
    fileFrom.append("chatpic", myfile);
    fileFrom.append("ename", enterpriseName);
    fileFrom.append("elogo", enterpriseLogo);
    fileFrom.append("speakerid", mySpeakerid);
    fileFrom.append("audienceid", myaudienceid);
    fileFrom.append("projectid", projectid);
    //上传图片到服务器
    $.ajax({
        type: "POST",
        contentType: false, //必须false才会避开jQuery对 formdata 的默认处理 , XMLHttpRequest会对 formdata 进行正确的处理
        processData: false, //必须false才会自动加上正确的Content-Type 
        url: '/ProjectFile/SaveUploadChatImg',
        data: fileFrom,
        success: function (data) {
            if (data != 0) {
                closeThis();
                window.location.href = "../Chat/Participation?uid=" + id + "&&pid=" + projectid + "";
            }
            else {
                message.alert("请重新尝试");
            }
        },
        error: function (msg) {
            message.alert("图片上传失败,请重新尝试！");
        }
    });
    //发送消息
    var sendMessage = strUrl.split(',');
    for (var i = 0; i < sendMessage.length; i++) {
        var options = {
            to: "kuaijing" + id,
            msg: sendMessage[i],
            type: "chat",
            ext: {
                enterpriseName: enterpriseName,
                enterpriseLogo: enterpriseLogo,
                projectId: projectid,
                projectType: "0",
                enterpriseId: $("#enpid").val(),
                projectUserId: id
            }
        };
        conn.sendTextMessage(options);
    }
}