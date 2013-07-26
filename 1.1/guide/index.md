## 综述

checkcode是依赖aliyun验证码服务的一个验证码组件，可同时实现图片、语音验证码显示、朗读、异步验证。

* 图片验证码支持数字+字母，纯数字两个方式。
* 语音验证码为4位数字
* 图片与语音验证码相互独立，无直接关系；语音验证码并不是图片验证码的语音版

** 接入前需申请identity ** 服务接口人：kj021320

## 快速使用 [demo](../demo/index.html)

### 初始化组件

    S.use('gallery/checkcode/1.1/index', function (S, Checkcode) {
        var checkcode = new Checkcode({
            input: "#J_CodeInput",
            container: "#J_CodeContainer",
            identity: "member1.taobao.com",
            sessionid: S.now(),
            type: "number"
        });
        
        // 显示图片验证码
        checkcode.showImg();

        // blur时校验验证码
        S.one("#J_CodeInput").on("blur", function(){
            checkcode.check(function(d) {
                if (d.success) {
                    alert((d.codeType === "IMG" ? "图片" : "语音") + "验证码验证成功！")
                }
                else {
                    alert((d.codeType === "IMG" ? "图片" : "语音") + "验证码验证失败！")
                }
            });
        });
    })

## API说明

### 参数说明

* input[Selector|HTMLElement]: 验证码输入框
* container[Selector|HTMLElement]: 验证码DOM渲染容器
* identity[String]: 验证码接入点id（联系kj021420申请）
* sessionid[String]: SessionID
* type[String]: 图片验证码类型


### 方法

#### showImg()

切换为显示图片验证码

#### showAudio()

切换为显示语音验证码

#### refresh()

刷新图片/语音验证码

#### check(callback)

验证验证码，callback参数作为验证完成回调；默认传入参数{success: Boolean, codeType: "IMG|AUDIO"}

具体见demo


### 事件

#### switch

图片/语音验证码切换时触发

#### refresh

图片/语音验证码刷新时触发
