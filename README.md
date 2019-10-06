## nike snkrs 分析



![2019-10-06-11-20-37](https://blog-oeynet-com.oss-cn-chengdu.aliyuncs.com/f1e8e905c6307852ab38b99d19dbd8eb.png)


![2019-10-06-11-22-30](https://blog-oeynet-com.oss-cn-chengdu.aliyuncs.com/7dff8a1ead7e7d3bb1b6482f8966028a.png)


数据监控: https://s3.nikecdn.com/public/80794486b1728205dd219006256bb



登录流程：

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



### 协议

授权协议：只允许研究、学习目的的分享、使用、修改，不允许任何商业用途。转载请注明出处，感谢。
