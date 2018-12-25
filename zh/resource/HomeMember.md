### 家庭成员管理类
### 调用API
#### `import TuyaHomeMemberApi from './api/TuyaHomeMemberApi'`

TuyaHomeMemberApi提供了家庭成员管理接口，包括添加、删除成员，更新成员的控制权限、获取家庭成员列表等.调用方式:`TuyaHomeMemberApi`(目前如果调用添加成员，此方法传参可传0，将在下个版本优化初始化和调用逻辑).家庭成员管理逻辑主要提供MemberBean用于获取成员信息的接口
```javascript 数据类型
	homeId; //家庭id
   nickName;//备注名
   admin;//是否是管理员
   memberId;//成员id
   headPic;//头像地址
   account;//成员账户名称
   uid;//成员唯一标识id
```

#### Home下面添加成员

```javascript
    /**
     * 给这个Home下面添加成员
     *
     * @param countryCode 国家码
     * @param userAccount 用户名
     * @param name        昵称
     * @param admin       是否拥有管理员权限
     * @param callback
     */
   TuyaHomeMemberApi.addMember({
	homeId:'',
	countryCode:'',//国家码,
	userAccount:'',//用户名,
	name:'',//昵称,
	admin:'',//是否拥有管理员权限
}).then(data=>{}).catch(e=>{})

```

#### 移除Home下面的成员

```javascript
   /**
     * 移除Home下面的成员
     *
     * @param id
     * @param callback
     */
    TuyaHomeMemberApi.removeMember({
	memberId:'',
}).then(data=>{}).catch(e=>{})
```

#### 更新成员备注名和权限
```javascript
/**
 * 更新成员备注名和权限
 * @param name 备注名 如果不更改备注名，传入从memberBean获取的nickName
 * @param admin  是否是管理员
 * @param callback
 */
TuyaHomeMemberApi.updateMember({
	memberId:'',
	name:'',//备注名,
	admin:'',//是否拥有管理员权限
}).then(data=>{}).catch(e=>{})
```

#### 查询Home下面的成员列表

```javascript
   /**
     * 查询Home下面的成员列表
     *
     * @param callback
     */
TuyaHomeMemberApi.queryMemberList({
	homeId:'',
}).then(data=>{}).catch(e=>{})
```