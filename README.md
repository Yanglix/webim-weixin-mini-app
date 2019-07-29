# webim-weixin-mini-app
小程序聊天demo 借鉴不少人 自己改了一个
#函数
initImParams: function (cbOk) {
        var that = this
        // 登录 初始化 im 参数
        // 注意：如果首次使用，后台需要创建【腾讯 im】账号
        wxLogin.wxGetLoginSession().then(()=>{
            wx.getUserInfo({
                success:(res)=> {
                    console.log(res,'fffdfasdfasfasfsa')
                    ajax.request({
                        data: {
                            serviceName: 'getUserSig',
                            token: wx.getStorageSync('sessionData'),//用户令牌
                        },
                        method: 'POST',
                        success: data => {
                            that.data.im.userSig = data.result.userSig
                            that.data.im.imId = data.result.identifier
                            // 初始化 im 数据
                            that.data.im.imName = res.userInfo.nickName
                            that.data.im.imAvatarUrl = res.userInfo.avatarUrl
                            cbOk()
                        },
                    })
                }
            })

        })
    },
    #配置对象
    data: {
        im: {
            sdkAppID: 564545644, // 用户标识接入 SDK 的应用 ID，必填
            accountType: 7878787, // 帐号体系集成中的 accountType，必填
            accountMode: 0, //帐号模式，0 - 独立模式 1 - 托管模式
            imId: null, // 用户的 id
            imName: null, // 用户的 im 名称
            imAvatarUrl: null, // 用户的 im 头像 url
            userSig: null, // 用户通过 imId 向后台申请的签名值 sig
        },
    },
    ###app.js 中加入

