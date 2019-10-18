## Nike Snkrs 分析

Before you read the project, you must understand the description of the project,

If the project infringes, please contact my email to delete this item

``` email
send email to (zhaojunlike@^FUCK/qq^FUCK.com).replace(/\^FUCK/g,"");
```

授权协议：只允许研究、学习目的的分享、使用、修改，不允许任何商业用途。转载请注明出处，感谢。


##  start

原文地址：https://github.com/zhaojunlike/nike-snkrs-api

该项目只提供思路不提供任何代码

> 1.Akamai ai risk control system 100% pass, 3-terminal data mock API optional

> 2.Cookie detection is 100% over provided by the generation API

> 3.Make sure that each sensor-data is very relevant


## web端思路
web端其实太简单了，mock一些事件和canvas就可以完成，所以如果你感兴趣可以看这个js文件：./mobile_files/80794486b1728205dd219006256bb.js ,
我做的数据来自于ios和android，他们使用了更复杂的算法，包括 Hardware sensors，It took me a long time to analyze。
``` typescript
// 所以你可以看到大概这样的代码
public static verifyFor103(total_b: number, r4: number, total_c: number, r0c: number): Long {

            let r9 = 32;
            let r8 = Long.fromNumber(total_b).shl(32);//右移动32位
            let r5: any = Long.fromNumber(total_c);
            let r15: any = 4294967295;
            r5 = r5.and(4294967295).or(r8);
            let r2 = r5.toInt(); //
            r5 = r5.shr(32).toInt();
            let r6 = r2;
            r2 = 0;
            let r30 = 0;
            while (true) {
                r15 = 16;
                if (r2 >= r15) break;
                let lr4 = Long.fromNumber(r4);
                r15 = lr4.shl(r2);
                let r16: any = 32 - r2;//减去
                r16 = lr4.shru(r16).toInt();
                r15 = r15.or(r16).xor(r6);
                r5 = Long.fromNumber(r5).xor(r15);
                r2++;
                r30 = r6;
                r6 = r5;
                r5 = r30;
            }
            let m9 = Long.fromNumber(r6).and(4294967295);
            return Long.fromNumber(r5).shl(32).xor(m9);
}

//又或者这个算法，能满足某些数据条件
 static fuck_a(fArr: Float32Array, i: number, i2: number, fArr2: Float32Array) {
            i2 = Math.floor(i2);
            i = Math.floor(i);
            if (i2 != 1) {
                let i3 = i2 / 2;
                for (let i4 = 0; i4 < i3; i4++) {
                    let i5 = i + i4;
                    let f = fArr[i5];
                    let f2 = fArr[((i + i2) - 1) - i4];
                    fArr2[i5] = f + f2;
                    let vv2 = ((i4 + 0.5) * 3.141592653589793);
                    fArr2[i5 + i3] = (f - f2) / (Math.cos(vv2 / i2) * 2.0);
                }
                this.fuck_a(fArr2, i, i3, fArr);
                let i6 = i + i3;
                this.fuck_a(fArr2, i6, i3, fArr);
                for (let i7 = 0; i7 < i3 - 1; i7++) {
                    let i8 = (i7 * 2) + i;
                    let i9 = i + i7;
                    fArr[i8 + 0] = fArr2[i9];
                    let i10 = i9 + i3;
                    fArr[i8 + 1] = fArr2[i10] + fArr2[i10 + 1];
                }
                let i11 = i + i2;
                fArr[i11 - 2] = fArr2[i6 - 1];
                let i12 = i11 - 1;
                fArr[i12] = fArr2[i12];
            }
}
```


下面该项目只提供演示api调用结果，目前实现功能：

-   [x] login api
-   [x] registry api
-   [x] launch/entries/v1
-   [x] cookies mock
-   [x] akamai data mock
-   [x] Automatic raising number


## steps 

tips：下面是一些简单的web端的逻辑流程，目前我没有看到akamai是否对web端有什么检测很严的影响，不过我相信，web端的数据模拟，你得懂很多算法，就如我之前说到的我做的腾讯滑块拖拽一样，它包含了加速度等等之类的信息，感兴趣的可以翻看我前面的文章，并且如果你不想自己去用代码实现mock，依赖selenium python,他没办法做到集群的，所以对于有几万个accounts的你，要考虑清楚是否使用简单的方案。

下面我提供登录流程思路：

```

1.访问登录页面

set-cookie: bm_sz=B37D70D8485724389F741A447D64272E~YAAQBWgDF6U8cJptAQAAW/fEngVzLQr34OcGkuRpuk4fkQXEwRg5Lm5HNVt/eX6LN3+MqPSQ8xRfoEtv8nKjfH+BIoPT1zlo5jKXftf04XKsq1I+ZxKjIpmcx7Eg8rxrVPOjmsMt9t73rkY722b2+xtnuf/Gp1ABBh6n+b4jDgKIbBQhEx/b5sPSUryZsVtToQ==; Domain=.nikecdn.com; Path=/; Expires=Sun, 06 Oct 2019 05:52:51 GMT; Max-Age=14400; HttpOnly
set-cookie: _abck=7FA9F8070CB4ECCF0D932306A0EE19EC~-1~YAAQBWgDF6Y8cJptAQAAW/fEngLnhueJqG/zWlL5St0uvc7Jq4H1rTTH+m5g7BInjI/x7P6G6wS1NU5+XlKM+mjRpQspjqGPcnc2p3btMBL5IjdLvoABWU5QeH2AWQW4zd0ko9s4d342xm5nebmCAt9Hg43UJsDHHFB5msUW+NlsM+0+qGsGxS3NDlagvxboOnOPG3TER3lj+4/gPO5IxVoS5zP5K3hJm8pFLhUOKA7oLD6D+6U4AcXwmlpdWy1Gm6vvU/Epz9S9lKWP5t/ZHEom/Pp4/NK4XWho9/ug4P0lCpAV2Vk50ZsIHw==~-1~-1~-1; Domain=.nikecdn.com; Path=/; Expires=Mon, 05 Oct 2020 01:52:51 GMT; Max-Age=31536000; Secure


2.注册cookie到sensor_data
GET
cookie: bm_sz=B37D70D8485724389F741A447D64272E~YAAQBWgDF6U8cJptAQAAW/fEngVzLQr34OcGkuRpuk4fkQXEwRg5Lm5HNVt/eX6LN3+MqPSQ8xRfoEtv8nKjfH+BIoPT1zlo5jKXftf04XKsq1I+ZxKjIpmcx7Eg8rxrVPOjmsMt9t73rkY722b2+xtnuf/Gp1ABBh6n+b4jDgKIbBQhEx/b5sPSUryZsVtToQ==
cookie: _abck=7FA9F8070CB4ECCF0D932306A0EE19EC~-1~YAAQBWgDF6Y8cJptAQAAW/fEngLnhueJqG/zWlL5St0uvc7Jq4H1rTTH+m5g7BInjI/x7P6G6wS1NU5+XlKM+mjRpQspjqGPcnc2p3btMBL5IjdLvoABWU5QeH2AWQW4zd0ko9s4d342xm5nebmCAt9Hg43UJsDHHFB5msUW+NlsM+0+qGsGxS3NDlagvxboOnOPG3TER3lj+4/gPO5IxVoS5zP5K3hJm8pFLhUOKA7oLD6D+6U4AcXwmlpdWy1Gm6vvU/Epz9S9lKWP5t/ZHEom/Pp4/NK4XWho9/ug4P0lCpAV2Vk50ZsIHw==~-1~-1~-1
x-requested-with: com.nike.snkrs


3.上传用户数据
post


4.进行登录

cookie: bm_sz=B37D70D8485724389F741A447D64272E~YAAQBWgDF6U8cJptAQAAW/fEngVzLQr34OcGkuRpuk4fkQXEwRg5Lm5HNVt/eX6LN3+MqPSQ8xRfoEtv8nKjfH+BIoPT1zlo5jKXftf04XKsq1I+ZxKjIpmcx7Eg8rxrVPOjmsMt9t73rkY722b2+xtnuf/Gp1ABBh6n+b4jDgKIbBQhEx/b5sPSUryZsVtToQ==
cookie: _abck=7FA9F8070CB4ECCF0D932306A0EE19EC~-1~YAAQBWgDF8A+cJptAQAAwTXFngKDLhcRfNXmKGRrcQj7GMBLX8ceaRQv3rrGvdx8bRxveQWFZIH/7UHoyZiITOYI3fRwGXXeoXxfEvLmuJb8KWC5Mba+ZLtzlDtdOXdkSOlwGxZK6GnnZW2Vw/YlfXhMovfyUdGnhtjDYDQWM9OpZvBupfHkpYkDbkj8wSd9+1TNjSRe/oKNLGCyrIVG6NE2EjfXtjVhdxwsV0R8sEm8k1+Tz3l7BSbTtETFM4h0ZQz7aLzKJjx2m5sBV3Zw2zYzhKNi7qRIuwY4xHcPFBAfYfkB1AKX2hXRRM7xjsxEmLT7Vh5VU6Nh/SFLGfVmYtPy/37J~-1~-1~-1
x-requested-with: com.nike.snkrs

//可能,如果登录失败，要么切换设备ID，要么上传错误信息后拿到cookie重新登录
https://unite.nike.com/error?platform=android&browser=uniteSDK&mobile=true&native=true&uxid=com.nike.commerce.snkrs.droid&locale=zh_CN&osVersion=24&sdkVersion=2.8.1&backendEnvironment=identity&url=https%3A%2F%2Fs3.nikecdn.com%2Flogin%3FappVersion%3D638%26experienceVersion%3D638%26uxid%3Dcom.nike.commerce.snkrs.droid%26locale%3Dzh_CN%26backendEnvironment%3Didentity%26browser%3DGoogle%2520Inc.%26os%3Dundefined%26mobile%3Dtrue%26native%3Dtrue%26visit%3D1%26visitor%3Dc36c3bfa-6700-43cd-bc7b-72a23c398b34&errorMsg=HTTP+error+message%3A++and+code%3A+401
```


