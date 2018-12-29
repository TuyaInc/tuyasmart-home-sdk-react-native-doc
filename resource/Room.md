###  房间管理类
### 调用API

####  `import {TuyaRoomApi} from 'tuyasmart-home-sdk'`

TuyaRoomApi 提供房间的管理类，负责房间的新增、删除设备或群组
可以通过 TuyaRoomApi 去创建

提供以下方法
- updateRoom 更新房间名称
- addDevice 添加设备
- removeDevice 删除设备
- removeGroup 删除群组

```java


    /**
     * 更新房间名称
     *
     * @param name     新房间名称
     * @param callback
     */
  TuyaRoomApi.updateRoom({
	roomId:'',
	name:''
   }).then(data=>{}).catch(e=>{})

    /**
     * 添加设备
     *
     * @param devId
     * @param callback
     */
TuyaRoomApi.addDevice({
	roomId:'',
	devId:''
}).then(data=>{}).catch(e=>{})

    /**
     * 添加群组
     *
     * @param groupId
     * @param callback
     */
TuyaRoomApi.addGroup({
	roomId:'',
	groupId:''
}).then(data=>{}).catch(e=>{})

    /**
     * 删除设备
     *
     * @param devId
     * @param callback
     */
TuyaRoomApi.removeDevice({
	roomId:'',
	devId:''
}).then(data=>{}).catch(e=>{})

    /**
     * 删除群组
     *
     * @param groupId
     * @param resultCallback
     */
  TuyaRoomApi.removeGroup({
	roomId:'',
	groupId:''
}).then(data=>{}).catch(e=>{})

    /**
     * 把群组或者设备移除房间
     *
     * @param list
     * @param callback
     */
    void moveDevGroupListFromRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback);

    /**
     * 对房间里的群组或者设备进行排序
     * @param list
     * @param callback
     */
    void sortDevInRoom(List<DeviceAndGroupInRoomBean> list, IResultCallback callback);

```