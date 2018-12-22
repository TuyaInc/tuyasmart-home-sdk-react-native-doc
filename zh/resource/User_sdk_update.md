### 1系列SDK账户迁移（非1系列用户可以忽略此步）
### 调用API
import TuyaUserApi from './api/TuyaUserApi'

需要登陆后在升级

```java
/**
* 检测是否要升级用户数据
*
* @return
*/
boolean checkVersionUpgrade();
    
/**
* 升级账号
/
void upgradeVersion(IResultCallback callback);
    
/**
*检测是否升级
*/
TuyaHomeSdk.getUserInstance().checkVersionUpgrade()
        
/**
*升级用户账号
*/
TuyaHomeSdk.getUserInstance().upgradeVersion()
```

