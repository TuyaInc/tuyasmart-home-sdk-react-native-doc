## 智能

### 调用API
import TuyaSceneApi from './api/TuyaSceneApi'

### 简介

智能分为场景和自动化。场景是用户添加动作，手动触发；自动化是由用户设定条件，当条件触发后自动执行设定的动作。

涂鸦智能Android SDK中，智能包括场景和自动化的统一管理接口

`TuyaSceneApi`


<strong>以下文档中手动场景和自动化场景简称为场景。</strong>

### 获取场景列表

##### 【描述】

获取场景列表，当场景首页初始化时使用。
##### 【方法原型】

```java
/**
 * 获取场景列表
 * @param homeId 家庭Id
 * @param callback 回调
 */
TuyaSceneApi.getSceneList({
	homeId:'',
})
```

其中，`Scene`返回的json值标识为如下

```js
/**
 *  获取场景id
 * @return 场景id
 */
id

/**
 *  获取场景名称
 * @return 场景名称
 */
Name

/**
 *  获取场景条件 
 * @return 场景条件 数组
 */
Conditions


/**
 *  获取场景任务
 * @return 场景任务 数组
 */
Actions
    
```

##### 【代码范例】

```js
TuyaSceneApi.getSceneList({
	homeId:'',
}).then(data=>{}).catch(e=>{})
```

### 自动化条件

用户可设置的条件包括天气状况、设备状况、定时。
​	
​	

- 天气型

	天气条件包括温度、湿度、天气、PM2.5、空气质量、日出日落， 可自由选定城市。根据用户账号中设备的不同，可选择的天气条件也不同。

	```js
	  /**
	   * 创建天气型条件
	   *
	   * @param place 天气城市 
	   * @param type  条件类型
	   * @param rule  条件规则
	   * @return
	   */
	  public static SceneCondition createWeatherCondition(
	      PlaceFacadeBean place, 
	      String type,
	      Rule rule)
	```

	  注: PlaceFacade类对象请从[获取城市列表](####10.2.4),[根据经纬度获取城市](####10.2.6), [根据城市id获取城市](####10.2.5)接口获取。
	​      目前获取城市接口只支持国内。

- 设备型

	设备条件是指当一个设备处于某种状态时，会触发另一台或多台设备的预定任务。<strong>为了避免循环控制，同一台设备无法同时作为条件和任务。</strong>

	```java
	  /**
	   * 创建设备型条件
	   *
	   * @param devBean 条件设备
	   * @param dpId    条件dpId
	   * @param rule    条件规则
	   * @return
	   */
	  public static SceneCondition createDevCondition(
	      SceneDevBean devBean,
	      String dpId,
	      Rule rule) 
	```

	  注: SceneDevBean类对象请从[获取条件设备列表](####10.2.2)接口获取。

- 定时

	定时指到达指定时间执行预定任务  

	```js
	/**
	  * 创建定时条件
	  * @param display 用于展示的用户选定的时间条件
	  * @param name  定时条件的名称
	  * @param type  条件类型
	  * @param rule  条件规则
	  * @return
	  */
	  public static SceneCondition createTimerCondition(String display,String name,String type,Rule rule)
	
	```

rule-条件规则有四种规则:
​	

- 数值型

	以温度为例，数值型条件的最终表达式为"temp > 20"的格式。您可以从获取条件列表接口获得目前支持的温度最大值、最小值、粒度（步进)，您可以从获取条件列表获取支持的温度等。在用户界面上完成配置后， 调用`ValueRule.newInstance`方法构建规则，并用规则构成条件。

	例:

	```java
	  ValueProperty tempProperty = (ValueProperty) conditionListBean.getProperty();       //数值型Property
	
	  int max = tempProperty.getMax();       //最大值
	  int min = tempProperty.getMin();       //最小值
	  int step = tempProperty.getStep();     //粒度
	  String unit = tempProperty.getUnit();  //单位
	
	//温度大于20度
	  ValueRule tempRule = ValueRule.newInstance(
	      "temp",  //类别
	      ">",     //运算规则(">", "==", "<")
	      20       //临界值
	  ); 
	SceneCondition tempCondition = SceneCondition.createWeatherCondition(
	      placeFacadeBean,   //城市
	      "temp",            //类别
	      tempRule           //规则
	  );
	```

	  

- 枚举型

	以天气状况为例, 枚举型条件的最终表达式为"condition == rainy"的格式，您可以从获取条件列表接口获得目前支持的天气状况，包括每种天气状况的code和名称。在用户界面上完成配置后， 调用`EnumRule.newInstance`方法构建规则，并用规则构成条件。

	例:

	```java
	  EnumProperty weatherProperty = (EnumProperty) conditionListBean.getProperty();  //枚举型Property
	
	  /** 
	  {
	     {"sunny", "晴天"},
	     {"rainy", "雨天"}
	  } 
	  */
	  HashMap<Object, String> enums = weatherProperty.getEnums();
	
	  //天气为下雨
	EnumRule enumRule = EnumRule.newInstance(
	              "condition",  //类别 
	              "rainy"        //选定的枚举值
	  );
	  SceneCondition weatherCondition = SceneCondition.createWeatherCondition(
	              placeFacadeBean,    //城市
	              "condition",        //类别
	              enumRule            //规则
	  );
	```

- 布尔型

	布尔型常见于设备型条件, 最终表达式为"dp1 == true"的格式, 您需要调用获取条件设备列表接口获取支持配置智能场景的设备， 然后根据设备id查询该设备可支持的操作，详见获取设备支持的操作。在用户界面上完成配置后， 调用`BoolRule.newInstance`方法构建规则，并用规则构成条件。

	例:

	```java
	BoolProperty devProperty = (BoolProperty) conditionListBean.getProperty();  //布尔型Property
	
	/**
	{
	  {true, "已开启"},
	  {false, "已关闭"}
	}
	*/
	HashMap<Boolean, String> boolMap = devProperty.getBoolMap(); 
	
	//当设备开启时
	BoolRule boolRule = BoolRule.newInstance(
	    "dp1",    //"dp" + dpId
	    true    //触发条件的bool
	);
	SceneCondition devCondition = SceneCondition.createDevCondition(
	    devBean,    //设备
	    "1",        //dpId
	    boolRule    //规则
	);
	```

- 定时型

	定时的表达式是Map类型，即Key：Value。当用户完成定时配置后，调用`TimerRule.newInstance`由SDK完成Map数据组装，构成规则条件。

	例：

	```java
	TimerProperty timerProperty = (TimerProperty)conditionListBean.
	getProperty();	//定时型property
	
	//TimerRule.newInstance 提供两个构造方法，区别是是否传入时区。
	//如果不传入时区将读取默认时区
	/**
	   * 
	   * @param timeZoneId 时区，格式例如"Asia/Shanghai"
	   * @param loops 7位字符串，每一位表示星期几，第一位表示星期日，第二位表示星期一，
	   * 依次类推，表示在哪些天启用定时。0表示未选中，1表示选中.格式例如只选中星期一
	   * 星期二："0110000"。如果都未选中，则表示定时只执行一次，格式："0000000"
	   * @param time 时间，24小时制。格式例如"08:00",如果用户使用12小时制，需要
	   * 开发者将之转换为24小时制上传
	   * @param date 日期，格式例如"20180310"
	   * @return
	   */
	  public static TimerRule newInstance(String timeZoneId,String loops,String time,String date);
	  
	  //构建定时规则
	  TimerRule timerRule = TimerRule.newInstance("Asia/Shanghai","0111110","16:00","20180310"
	  
	  
	  /**
	   * 所需要的参数与上述方法的参数意义相同，读取默认时区
	   * @param loops
	   * @param time
	   * @param date
	   * @return
	   */
	  public static TimerRule newInstance(String loops,String time,String date);
	  
	  /**
	   * 创建定时条件
	   * @param display 用于展示给用户的选定的时间
	   * @param name  定时条件的名称
	   * @param type  条件类型
	   * @param rule  条件规则
	   * @return
	   */
	  public static SceneCondition createTimerCondition(String display,String name,String type,Rule rule);
	  
	  //创建定时条件,以上面构建的定时规则为例
	  SceneCondition.createTimerCondition(
	  "周一周二周三周四周五",
	  "工作日定时",
	  "timer",
	  timerRule
	  )
	
	```

#### 获取条件列表

##### 【接口描述】

获取当前用户支持配置的条件的列表，通常用于添加或修改条件的第一步。

##### 【方法原型】

```java
/**
 * 获取条件列表
 * @param showFahrenheit 是否显示华氏度
 * @param callback 回调
 */
void getConditionList(boolean showFahrenheit,ITuyaResultCallback<List<ConditionListBean>> callback);
```

其中， `ConditionListBean`提供的接口为

```java
/**
 * 获取条件类别
 *
 * @return 类别 [1]
 */
public String getType() {
    return type;
}·

/**
 * 获取条件名称
 *
 * @return 名称
 */
public String getName() {
    return name;
}

/**
 * 获取Property [2]
 *
 * @return Property 
 */
public IProperty getProperty() {
    return property;
} 
```

<strong>注:</strong>

1. 目前支持的天气条件类别及其名称和Property类型

	| 名称     | Type       | Property Type |
	| -------- | ---------- | ------------- |
	| 温度     | Temp       | ValueProperty |
	| 湿度     | humidity   | EnumProperty  |
	| 天气     | condition  | EnumProperty  |
	| PM2.5    | pm25       | EnumProperty  |
	| 空气质量 | aqi        | EnumProperty  |
	| 日出日落 | sunsetrise | EnumProperty  |
	| 定时     | timer      | TimerProperty |

2. Property是涂鸦智能中一种常用的数据结构，可以用来控制设备和其他功能。目前提供四种Property: 数值型，枚举型，布尔型和用于定时的类型(与条件中的数值型，枚举型，布尔型相对应), 每种Property提供不同的访问接口。详见前文规则介绍处。

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getConditionList(new ITuyaDataCallback<List<ConditionListBean>>() {
    @Override
    public void onSuccess(List<ConditionListBean> conditionActionBeans) {
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

#### 获取条件设备列表

##### 【描述】

获取可用于条件设置的设备列表。

##### 【方法原型】

```java
/**
 * 获取条件中的可选设备列表
 * @param homeId 家庭的id
 * @param callback 回调
 */
void getConditionDevList(long homeId, ITuyaResultCallback<List<DeviceBean>> callback);
```

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getConditionDevList(homeId ,new ITuyaResultCallback<List<DeviceBean>>() {
    @Override
    public void onSuccess(List<DeviceBean> deviceBeans) {
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

#### 根据设备id获取设备任务

##### 【描述】

用于获取在选择设备具体的触发条件时， 可选择的任务。

##### 【方法原型】

```java
  /**
     * 获取设备支持的任务条件列表
     *
     * @param devId    设备id
     * @param callback 回调
     */
    void getDeviceConditionOperationList(String devId, ITuyaResultCallback<List<TaskListBean>> callback);
```

其中, `TaskListBean`提供以下接口:

```java
/**
 *  获取dp点名称， 用于界面展示
 *
 * @return dp点名称
 */
public String getName() {
    return name;
}

/**
 *  获取dpId
 *
 * @return dpId
 */
public long getDpId() {
    return dpId;
}

/**
 *  获取该dp点可配置的操作
 *
 *   格式:
 *     {
 *       {true, "已开启"},
 *       {false, "已关闭"}
 *     }
 *
 * @return 
 */
public HashMap<Object, String> getTasks() {
    return tasks;
}
/**
 *  获取该条件的类型bool、value、enum等
 */
public String getType() {
    return type;
}
```

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getDeviceConditionOperationList(
    devId, //设备id
    new ITuyaDataCallback<List<TaskListBean>>() {
        @Override
        public void onSuccess(List<TaskListBean> conditionActionBeans) {
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
}
```

#### 获取城市列表

##### 【描述】

用于在创建天气条件时，选择城市。
注： 目前城市列表暂时仅支持中国。

##### 【方法原型】

```java
/**
 * 根据国家码获取城市列表
 *
 * @param countryCode 国家码
 * @param callback    回调
 */
void getCityListByCountryCode(String countryCode, ITuyaResultCallback<List<PlaceFacadeBean>> callback);
```

其中, `PlaceFacadeBean`类提供以下接口:

```java
/**
 * 获取区域名称
 *
 * @return 区域名称
 */
public String getArea() {
    return area;
}

/**
 * 获取省份名称
 *
 * @return 省份名称
 */
public String getProvince() {
    return province;
}

/**
 * 获取城市名称
 *
 * @return 城市名称
 */
public String getCity() {
    return city;
}

/**
 * 获取城市id
 *
 * @return 城市id
 */
public long getCityId() {
    return cityId;
}
```

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getCityListByCountryCode(
	"cn",  //中国
	new ITuyaResultCallback<List<PlaceFacadeBean>>() {
    	@Override
    	public void onSuccess(List<PlaceFacadeBean> placeFacadeBeans) {
    	}

    	@Override
    	public void onError(String errorCode, String errorMessage) {
    	}
});
```

#### 根据城市id获取城市信息

##### 【描述】

根据城市id获取城市信息， 用于展示已有的天气条件。城市id可以在获取城市列表接口中获取。

##### 【方法原型】

```java
/**
 * 根据城市id获取城市信息
 *
 * @param cityId   城市id{@link PlaceFacadeBean}
 * @param callback 回调
 */
void getCityByCityIndex(long cityId, ITuyaResultCallback<PlaceFacadeBean> callback);
```

#### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getCityByCityIndex(
	cityId, //城市id
	new ITuyaResultCallback<PlaceFacadeBean>() {
		@Override
		public void onSuccess(PlaceFacadeBean placeFacadeBean) {
		}

		@Override
		public void onError(String errorCode, String errorMessage) {
		}
});
```

#### 根据经纬度获取城市信息

##### 【描述】

根据经纬度获取城市信息， 用于展示已有的天气条件。

##### 【方法原型】

```java
/**
 * 根据经纬度获取城市信息
 *
 * @param lon      经度
 * @param lat      纬度
 * @param callback 回调
 */
void getCityByLatLng(String lon, String lat, ITuyaResultCallback<PlaceFacadeBean> callback);
```

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getCityByLatLng(
    String.valueOf(longitude), //经度
    String.valueOf(latitude),   //纬度
    new ITuyaResultCallback<PlaceFacadeBean>() {
        @Override
        public void onSuccess(PlaceFacadeBean placeFacadeBean) {
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```

### 场景动作

场景动作指当条件触发时执行的控制设备动作。手动场景可执行的动作包含自动化场景和智能设备，自动化场景可执行的动作包含手动场景、其他自动化场景和智能设备。用户可设定的任务视用户的设备而定，请注意，并不是每一款产品都支持场景。

#### 创建动作

##### 【描述】

用于创建场景动作。

##### 【方法原型】

```java
/**
 * 创建场景动作
 *
 * @param devId 设备id
 * @param tasks 要执行的任务 格式: { dpId: dp点值 }
 *                          例：
 *                          {
 *                              "1": true,
 *                          }
 * @return 场景动作
 */
public static SceneTask createDpTask(@NonNull String devId, HashMap<String, Object> tasks)

```

##### 【代码范例】

```java
HashMap<String, Object> taskMap = new HashMap<>();
taskMap.put("1", true); //开启设备
SceneTask task = SceneTask.createDpTask(
    devId,      //设备id
    taskMap     //设备动作
);
```

#### 获取执行动作支持的设备列表

##### 【描述】

获取支持场景动作的设备列表， 用于选择添加到要执行的动作中。

##### 【方法原型】

```java
/**
 * 获取动作中的可选设备列表
 * @param homeId 家庭id
 * @param callback 回调
 */
void getTaskDevList(long homeId, ITuyaResultCallback<List<DeviceBean>> callback);
```

其中， `DeviceBean `提供以下接口:

```java
/**
 *  获取设备名称
 * 
 * @return 设备名称
 */
public String getName() {
    return name;
}

/**
 *  产品id
 * 
 * @return 产品id
 */
public String getProductId() {
    return productId;
}

/**
 *  获取设备id
 * 
 * @return 设备id
 */
public String getDevId() {
    return devId;
}

/**
 *  获取设备图标
 * 
 * @return 图标地址
 */
public String getIconUrl() {
     return iconUrl;
 }
```

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getTaskDevList(new ITuyaResultCallback<List<DeviceBean>>() {
    @Override
    public void onSuccess(List<DeviceBean> deviceBeans) {
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

#### 根据设备id获取可执行的动作

##### 【描述】

用于在创建动作时， 获取设备可执行的任务。设备id可以从[获取执行动作支持的设备列表](####10.3.1)获取

##### 【方法原型】

```java
/**
* 获取设备可以执行的操作
*
* @param devId    设备id
* @param callback 回调
*/
void getDeviceTaskOperationList(String devId, ITuyaResultCallback<List<TaskListBean>> callback);
```

其中, `TaskListBean`提供以下接口:

```java
/**
 *  获取dp点名称， 用于界面展示
 *
 * @return dp点名称
 */
public String getName() {
    return name;
}

/**
 *  获取dpId
 *
 * @return dpId
 */
public long getDpId() {
    return dpId;
}

/**
 *  获取该dp点可配置的操作
 *
 *   格式:
 *     {
 *       {true, "已开启"},
 *       {false, "已关闭"}
 *     }
 *
 * @return 
 */
public HashMap<Object, String> getTasks() {
    return tasks;
}
/**
 *  获取该条件的类型bool、value、enum等
 */
public String getType() {
    return type;
}

```

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().getTaskList(
    devId, //设备id
    new ITuyaResultCallback<List<TaskListBean>>() {
        @Override
        public void onSuccess(List<TaskListBean> conditionActionBeans) {
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```

### 创建场景

##### 【描述】

用于将条件和动作组装成场景并创建新的场景， 成功后会返回场景数据。
两种创建方法，相对应的涂鸦的场景和自动化 一个没带条件conditionList，一个有带conditionList

##### 【方法原型】

```java
/**
 * 创建场景
 *
 * @param homeId	  家庭id
 * @param name       场景名称
 * @param stickyOnTop 是否显示在首页
 * @param devIds 设备列表
 * @param conditions 场景触发条件 {@link SceneCondition}
 * @param tasks      ActionList {@link SceneTask}
 * @param matchType  场景条件与或关系  SceneBean.MATCH_TYPE_OR 表示满足任意条件执行，默认值；SceneBean.MATCH_TYPE_AND 表示满足所有条件
 */
  TuyaSceneApi.createScene({
              homeId: '',
              name: this.state.name,
              stickyOnTop: false,
              devIds: devLists,
              background: "a",
              matchType: "MATCH_TYPE_OR",
              tasks: ActionLists
            })
```

```java
/**
 * 创建场景
 *
 * @param homeId	  家庭id
 * @param name       场景名称
 * @param conditions 场景触发条件 {@link SceneCondition}
 * @param tasks      场景执行任务 {@link SceneTask}
 * @param matchType  场景条件与或关系  SceneBean.MATCH_TYPE_OR 表示满足任意条件执行，默认值；SceneBean.MATCH_TYPE_AND 表示满足所有条件
 * @param callback   回调
 */
    TuyaSceneApi.createAutoScene({
              homeId: "",
              name: this.state.name,
              stickyOnTop: false,
              devIds: devLists,
              background: "a",
              matchType: "MATCH_TYPE_OR",
              tasks: ActionLists,
              conditionList:this.state.ConditionList
            })

```

##### 【代码范例】

```js
//场景
     TuyaSceneApi.createScene({
              homeId: 100001,
              name: this.state.name,
              stickyOnTop: false,
              devIds: devLists,
              background: "a",
              matchType: "MATCH_TYPE_OR",
              tasks: ActionLists
            })
              .then(data => {
                console.log("--->data", data);
                DeviceStorage.delete("Action");
                this.props.navigation.navigate("HomePage");
              })
              .catch(err => {
                console.log("-->err", err);
              });

//自动化
      TuyaSceneApi.createAutoScene({
              homeId: 100001,
              name: this.state.name,
              stickyOnTop: false,
              devIds: devLists,
              background: "a",
              matchType: "MATCH_TYPE_OR",
              tasks: ActionLists,
              conditionList:this.state.ConditionList
            })
              .then(data => {
                console.log("--->data", data);

              })
              .catch(err => {
                console.log("-->err", err);
              });
```

### 10.5 修改场景

##### 【描述】

用于修改场景， 成功后会返回新的场景数据。

##### 【方法原型】

```java
/**
 *  修改场景
 * 
 * @param sceneReqBean 场景数据类
 * @param callback 回调
 */
void modifyScene(SceneBean sceneReqBean, ITuyaResultCallback<SceneBean> callback);
```

注：
该接口只能用于修改场景，请勿传入新建的SceneBean对象。

##### 【代码范例】

```java
sceneBean.setName("New name");  //更改场景名称
sceneBean.setConditions(Collections.singletonList(condition)); //更改场景条件
sceneBean.setActions(tasks); //更改场景动作

String sceneId = sceneBean.getId();  //获取场景id以初始化
TuyaHomeSdk.newSceneInstance(sceneId).modifyScene(
    sceneBean,  //修改后的场景数据类
    new ITuyaResultCallback<SceneBean>() {
        @Override
        public void onSuccess(SceneBean sceneBean) {
            Log.d(TAG, "Modify Scene Success");
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```

### 执行场景

##### 【描述】

用于执行手动场景。

##### 【方法原型】

```java
/**
 * 执行场景动作
 *
 * @param callback 回调
 */
void executeScene(IResultCallback callback);
```

##### 【代码范例】

```java
String sceneId = sceneBean.getId();  

TuyaHomeSdk.newSceneInstance(sceneId).executeScene(new IResultCallback() {
    @Override
    public void onSuccess() {
        Log.d(TAG, "Excute Scene Success");
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

### 删除场景

##### 【描述】

用于删除场景。

##### 【方法原型】

```java
/**
 * 删除场景
 *
 * @param callback 回调
 */
void deleteScene(IResultCallback callback);
```

##### 【代码范例】

```java
String sceneId = sceneBean.getId();  

TuyaHomeSdk.newSceneInstance(sceneId).deleteScene(new 
IResultCallback() {
    @Override
    public void onSuccess() {
        Log.d(TAG, "Delete Scene Success");
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

### 开启关闭自动化场景

##### 【描述】

用于开启或关闭自动化场景

##### 【方法原型】

```java
/**
 * 开启自动化场景
 * @param sceneId  
 * @param callback 回调
 */
void enableScene(String sceneId, final IResultCallback callback);

```

```java
/**
 * 关闭自动化场景
 * @param sceneId  
 * @param callback 回调
 */
void disableScene(String sceneId, final IResultCallback callback);

```

##### 【代码范例】

```java
String sceneId = sceneBean.getId();  

TuyaHomeSdk.newSceneInstance(sceneId).enableScene(sceneId,new 
IResultCallback() {
    @Override
    public void onSuccess() {
        Log.d(TAG, "enable Scene Success");
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});

TuyaHomeSdk.newSceneInstance(sceneId).disableScene(sceneId,new 
IResultCallback() {
    @Override
    public void onSuccess() {
        Log.d(TAG, "disable Scene Success");
    }

    @Override
    public void onError(String errorCode, String errorMessage) {
    }
});
```

### 场景排序

##### 【描述】

手动场景或自动化场景排序。注意：只能单独对手动场景或自动化场景排序，不能混排。

##### 【方法原型】

```java
/**
 * 场景排序
 * @param homeId 家庭id
 * @param sceneIds 手动场景或自动化场景已排序好的的id列表
 * @param callback    回调
 */
void sortSceneList(long homeId, List<String> sceneIds, IResultCallback callback)
```

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().sortSceneList(
    homeId, //家庭列表
    sceneIds,//场景id列表
    new IResultCallback() {
        @Override
        public void onSuccess() {
        }

        @Override
        public void onError(String errorCode, String errorMessage) {
        }
});
```

### 销毁

##### 【描述】

如果退出场景的activity，应该调用场景的销毁方法，以回收内存，提升体验

##### 【代码范例】

```java
TuyaHomeSdk.getSceneManagerInstance().onDestroy();

TuyaHomeSdk.newSceneInstance(sceneId).onDestroy();
```

## 