### 1系列SDK账户迁移（非1系列用户可以忽略此步）
### 调用API
####  `import {TuyaUserApi} from 'tuyasmart-home-sdk'`


需要登陆后在升级

```js
/**
* 检测是否要升级用户数据
*
* @return
*/
TuyaUserApi.checkVersionUpgrade({}).then(data=>{
}).catch(err=>{
})
    
/**
* 升级账号
/
TuyaUserApi.upgradeVersion({}).then(data=>{
}).catch(err=>{
})

```

