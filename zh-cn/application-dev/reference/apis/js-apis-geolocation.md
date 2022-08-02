# 位置服务

位置服务提供GNSS定位、网络定位、地理编码、逆地理编码、国家码和地理围栏等基本功能。

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```js
import geolocation from '@ohos.geolocation';
```

## geolocation.on('locationChange')

on(type: 'locationChange', request: LocationRequest, callback: Callback&lt;Location&gt;) : void

开启位置变化订阅，并发起定位请求。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationChange”，表示位置变化。 |
  | request | LocationRequest | 是 | 设置位置请求参数。 |
  | callback | Callback&lt;[Location](#location)&gt; | 是 | 接收位置变化状态变化监听。 |
  


**示例**
  
  ```js
  var requestInfo = {'priority': 0x203, 'scenario': 0x300, 'timeInterval': 0, 'distanceInterval': 0, 'maxAccuracy': 0};
  var locationChange = (location) => {
      console.log('locationChanger: data: ' + JSON.stringify(location));
  };
  geolocation.on('locationChange', requestInfo, locationChange);
  ```


## geolocation.off('locationChange')

off(type: 'locationChange', callback?: Callback&lt;Location&gt;) : void

关闭位置变化订阅，并删除对应的定位请求。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationChange”，表示位置变化。 |
  | callback | Callback&lt;[Location](#location)&gt; | 否 | 接收位置变化状态变化监听。 |


**示例**
  
  ```js
  var requestInfo = {'priority': 0x203, 'scenario': 0x300, 'timeInterval': 0, 'distanceInterval': 0, 'maxAccuracy': 0};
  var locationChange = (location) => {
      console.log('locationChanger: data: ' + JSON.stringify(location));
  };
  geolocation.on('locationChange', requestInfo, locationChange);
  geolocation.off('locationChange', locationChange);
  ```


## geolocation.on('locationServiceState')

on(type: 'locationServiceState', callback: Callback&lt;boolean&gt;) : void

订阅位置服务状态变化。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数：**

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationServiceState”，表示位置服务状态。 |
  | callback | Callback&lt;boolean&gt; | 是 | 接收位置服务状态变化监听。 |


**示例**
  
  ```js
  var locationServiceState = (state) => {
      console.log('locationServiceState: ' + JSON.stringify(state));
  }
  geolocation.on('locationServiceState', locationServiceState);
  ```


## geolocation.off('locationServiceState')

off(type: 'locationServiceState', callback?: Callback&lt;boolean&gt;) : void;

取消订阅位置服务状态变化。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“locationServiceState”，表示位置服务状态。 |
  | callback | Callback&lt;boolean&gt; | 否 | 接收位置服务状态变化监听。 |


**示例**
  
  ```js
  var locationServiceState = (state) => {
      console.log('locationServiceState: state: ' + JSON.stringify(state));
  }
  geolocation.on('locationServiceState', locationServiceState);
  geolocation.off('locationServiceState', locationServiceState);
  ```


## geolocation.on('cachedGnssLocationsReporting')<sup>8+</sup>

on(type: 'cachedGnssLocationsReporting', request: CachedGnssLocationsRequest, callback: Callback&lt;Array&lt;Location&gt;&gt;) : void;

订阅缓存GNSS定位结果上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“cachedGnssLocationsReporting”，表示GNSS缓存定位结果上报。 |
  | request | CachedGnssLocationsRequest | 是 | GNSS缓存功能配置参数 |
  | callback | Callback&lt;boolean&gt; | 是 | 接收GNSS缓存位置上报。 |


**示例**
  
  ```js
  var cachedLocationsCb = (locations) => {
      console.log('cachedGnssLocationsReporting: locations: ' + JSON.stringify(locations));
  }
  var requestInfo = {'reportingPeriodSec': 10, 'wakeUpCacheQueueFull': true};
  geolocation.on('cachedGnssLocationsReporting', requestInfo, cachedLocationsCb);
  ```


## geolocation.off('cachedGnssLocationsReporting')<sup>8+</sup>

off(type: 'cachedGnssLocationsReporting', callback?: Callback&lt;Array&lt;Location&gt;&gt;) : void;

取消订阅缓存GNSS定位结果上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“cachedGnssLocationsReporting”，表示GNSS缓存定位结果上报。 |
  | callback | Callback&lt;boolean&gt; | 否 | 接收GNSS缓存位置上报。 |


**示例**
  
  ```js
  var cachedLocationsCb = (locations) => {
      console.log('cachedGnssLocationsReporting: locations: ' + JSON.stringify(locations));
  }
  var requestInfo = {'reportingPeriodSec': 10, 'wakeUpCacheQueueFull': true};
  geolocation.on('cachedGnssLocationsReporting', requestInfo, cachedLocationsCb);
  geolocation.off('cachedGnssLocationsReporting');
  ```


## geolocation.on('gnssStatusChange')<sup>8+</sup>

on(type: 'gnssStatusChange', callback: Callback&lt;SatelliteStatusInfo&gt;) : void;

订阅GNSS卫星状态信息上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“gnssStatusChange”，表示订阅GNSS卫星状态信息上报。 |
  | callback | Callback&lt;SatelliteStatusInfo&gt; | 是 | 接收GNSS卫星状态信息上报。 |


**示例**
  
  ```js
  var gnssStatusCb = (satelliteStatusInfo) => {
      console.log('gnssStatusChange: ' + JSON.stringify(satelliteStatusInfo));
  }
  geolocation.on('gnssStatusChange', gnssStatusCb);
  ```


## geolocation.off('gnssStatusChange')<sup>8+</sup>

off(type: 'gnssStatusChange', callback?: Callback&lt;SatelliteStatusInfo&gt;) : void;

取消订阅GNSS卫星状态信息上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“gnssStatusChange”，表示订阅GNSS卫星状态信息上报。 |
  | callback | Callback&lt;SatelliteStatusInfo&gt; | 否 | 接收GNSS卫星状态信息上报。 |

**示例**
  
  ```js
  var gnssStatusCb = (satelliteStatusInfo) => {
      console.log('gnssStatusChange: ' + JSON.stringify(satelliteStatusInfo));
  }
  geolocation.on('gnssStatusChange', gnssStatusCb);
  geolocation.off('gnssStatusChange', gnssStatusCb);
  ```


## geolocation.on('nmeaMessageChange')<sup>8+</sup>

on(type: 'nmeaMessageChange', callback: Callback&lt;string&gt;) : void;

订阅GNSS NMEA信息上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“nmeaMessageChange”，表示订阅GNSS&nbsp;NMEA信息上报。 |
  | callback | Callback&lt;string&gt; | 是 | 接收GNSS&nbsp;NMEA信息上报。 |


**示例**
  
  ```js
  var nmeaCb = (str) => {
      console.log('nmeaMessageChange: ' + JSON.stringify(str));
  }
  geolocation.on('nmeaMessageChange', nmeaCb );
  ```


## geolocation.off('nmeaMessageChange')<sup>8+</sup>

off(type: 'nmeaMessageChange', callback?: Callback&lt;string&gt;) : void;

取消订阅GNSS NMEA信息上报事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“nmeaMessageChange”，表示订阅GNSS&nbsp;NMEA信息上报。 |
  | callback | Callback&lt;string&gt; | 否 | 接收GNSS&nbsp;NMEA信息上报。 |


**示例**
  
  ```js
  var nmeaCb = (str) => {
      console.log('nmeaMessageChange: ' + JSON.stringify(str));
  }
  geolocation.on('nmeaMessageChange', nmeaCb);
  geolocation.off('nmeaMessageChange', nmeaCb);
  ```


## geolocation.on('fenceStatusChange')<sup>8+</sup>

on(type: 'fenceStatusChange', request: GeofenceRequest, want: WantAgent) : void;

添加一个围栏，并订阅地理围栏事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“fenceStatusChange”，表示订阅围栏事件上报。 |
  | request | GeofenceRequest | 是 | 围栏的配置参数。 |
  | want | WantAgent | 是 | 用于接收地理围栏事件上报（进出围栏）。 |


**示例**
  
  ```js
  import geolocation from '@ohos.geolocation';
  import wantAgent from '@ohos.wantAgent';
  
  let wantAgentInfo = {
      wants: [
          {
              bundleName: "com.example.myapplication",
              abilityName: "com.example.myapplication.MainAbility"
              action: "action1",
          }
      ],
      operationType: wantAgent.OperationType.START_ABILITY,
      requestCode: 0,
      wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
  };
  
  wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
    var requestInfo = {'priority': 0x201, 'scenario': 0x301, "geofence": {"latitude": 121, "longitude": 26, "radius": 100, "expiration": 10000}};
    geolocation.on('fenceStatusChange', requestInfo, wantAgentObj);
  });
  ```


## geolocation.off('fenceStatusChange')<sup>8+</sup>

off(type: 'fenceStatusChange', request: GeofenceRequest, want: WantAgent) : void;

删除一个围栏，并取消订阅该围栏事件。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“fenceStatusChange”，表示订阅围栏事件上报。 |
  | request | GeofenceRequest | 是 | 围栏的配置参数。 |
  | want | WantAgent | 是 | 用于接收地理围栏事件上报（进出围栏）。 |

**示例**
  
  ```js
  import geolocation from '@ohos.geolocation';
  import wantAgent from '@ohos.wantAgent';
  
  let wantAgentInfo = {
      wants: [
          {
              bundleName: "com.example.myapplication",
              abilityName: "com.example.myapplication.MainAbility"
              action: "action1",
          }
      ],
      operationType: wantAgent.OperationType.START_ABILITY,
      requestCode: 0,
      wantAgentFlags: [wantAgent.WantAgentFlags.UPDATE_PRESENT_FLAG]
  };
  
  wantAgent.getWantAgent(wantAgentInfo).then((wantAgentObj) => {
    var requestInfo = {'priority': 0x201, 'scenario': 0x301, "geofence": {"latitude": 121, "longitude": 26, "radius": 100, "expiration": 10000}};
    geolocation.on('fenceStatusChange', requestInfo, wantAgentObj);
    geolocation.off('fenceStatusChange', requestInfo, wantAgentObj);
  });
  ```


## geolocation.on('countryCodeChange')<sup>9+</sup>

on(type: 'countryCodeChange', callback: Callback&lt;CountryCode&gt;) : void;

订阅国家码信息上报事件。

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“countryCodeChange”，表示订阅国家码信息上报。 |
  | callback | Callback&lt;CountryCode&gt; | 是 | 接收国家码信息上报。 |


**示例**
  
  ```js
  var callback = (code) => {
      console.log('countryCodeChange: ' + JSON.stringify(code));
  }
  geolocation.on('countryCodeChange', callback);
  ```


## geolocation.off('countryCodeChange')<sup>9+</sup>

off(type: 'countryCodeChange', callback?: Callback&lt;CountryCode&gt;) : void;

取消订阅国家码上报事件。

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | string | 是 | 设置事件类型。type为“countryCodeChange”，表示取消订阅国家码信息上报。 |
  | callback | Callback&lt;CountryCode&gt; | 是 | 接收国家码信息上报。 |


**示例**
  
  ```js
  var callback = (code) => {
      console.log('countryCodeChange: ' + JSON.stringify(code));
  }
  geolocation.on('countryCodeChange', callback);
  geolocation.off('countryCodeChange', callback);
  ```


## geolocation.getCurrentLocation

getCurrentLocation(request: CurrentLocationRequest, callback: AsyncCallback&lt;Location&gt;) : void


获取当前位置，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [CurrentLocationRequest](#currentlocationrequest) | 否 | 设置位置请求参数。 |
  | callback | AsyncCallback&lt;[Location](#location)&gt; | 是 | 用来接收位置信息的回调。 |

**示例**
  
  ```js
  var requestInfo = {'priority': 0x203, 'scenario': 0x300,'maxAccuracy': 0};
  var locationChange = (err, location) => {
      if (err) {
          console.log('locationChanger: err=' + JSON.stringify(err));
      }
      if (location) {
          console.log('locationChanger: location=' + JSON.stringify(location));
      }
  };
  geolocation.getCurrentLocation(requestInfo, locationChange);
  geolocation.getCurrentLocation(locationChange);
  ```


## geolocation.getCurrentLocation

getCurrentLocation(request?: CurrentLocationRequest) : Promise&lt;Location&gt;


获取当前位置，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [CurrentLocationRequest](#currentlocationrequest) | 否 | 设置位置请求参数。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;[Location](#location)&gt; | 返回位置信息。 |


**示例**
  
  ```js
  var requestInfo = {'priority': 0x203, 'scenario': 0x300,'maxAccuracy': 0};
  geolocation.getCurrentLocation(requestInfo).then((result) => {
      console.log('current location: ' + JSON.stringify(result));
  });
  ```


## geolocation.getLastLocation

getLastLocation(callback: AsyncCallback&lt;Location&gt;) : void

获取上一次位置，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[Location](#location)&gt; | 是 | 用来接收上次位置的回调。 |


**示例**
  
  ```js
  geolocation.getLastLocation((err, data) => {
      if (err) {
          console.log('getLastLocation: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('getLastLocation: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.getLastLocation

getLastLocation() : Promise&lt;Location&gt;

获取上一次位置，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;[Location](#location)&gt; | 返回上次位置信息。 |


**示例**
  
  ```js
  geolocation.getLastLocation().then((result) => {
      console.log('getLastLocation: result: ' + JSON.stringify(result));
  });
  ```


## geolocation.isLocationEnabled

isLocationEnabled(callback: AsyncCallback&lt;boolean&gt;) : void


判断位置服务是否已经打开，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |

**示例**
  
  ```js
  geolocation.isLocationEnabled((err, data) => {
      if (err) {
          console.log('isLocationEnabled: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('isLocationEnabled: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.isLocationEnabled

isLocationEnabled() : Promise&lt;boolean&gt;

判断位置服务是否已经开启，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回位置服务是否可用的状态。 |

**示例**
  
  ```js
  geolocation.isLocationEnabled().then((result) => {
      console.log('promise, isLocationEnabled: ' + JSON.stringify(result));
  });
  ```


## geolocation.requestEnableLocation

requestEnableLocation(callback: AsyncCallback&lt;boolean&gt;) : void


请求打开位置服务，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |

**示例**
  
  ```js
  geolocation.requestEnableLocation((err, data) => {
      if (err) {
          console.log('requestEnableLocation: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('requestEnableLocation: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.requestEnableLocation

requestEnableLocation() : Promise&lt;boolean&gt;

请求打开位置服务，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回位置服务是否可用。 |

**示例**
  
  ```js
  geolocation.requestEnableLocation().then((result) => {
      console.log('promise, requestEnableLocation: ' + JSON.stringify(result));
  });
  ```


## geolocation.enableLocation

enableLocation(callback: AsyncCallback&lt;boolean&gt;) : void;

打开位置服务，使用callback回调异步返回结果。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |

**示例**
  
  ```js
  geolocation.enableLocation((err, data) => {
      if (err) {
          console.log('enableLocation: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('enableLocation: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.enableLocation

enableLocation() : Promise&lt;boolean&gt;

打开位置服务，使用Promise方式异步返回结果。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回位置服务是否可用。 |

**示例**
  
  ```js
  geolocation.enableLocation().then((result) => {
      console.log('promise, enableLocation: ' + JSON.stringify(result));
  });
  ```

## geolocation.disableLocation

disableLocation(callback: AsyncCallback&lt;boolean&gt;) : void;

关闭位置服务，使用callback回调异步返回结果。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收位置服务状态的回调。 |

**示例**
  
  ```js
  geolocation.disableLocation((err, data) => {
      if (err) {
          console.log('disableLocation: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('disableLocation: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.disableLocation

disableLocation() : Promise&lt;boolean&gt;

关闭位置服务，使用Promise方式异步返回结果。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.MANAGE_SECURE_SETTINGS

**系统能力**：SystemCapability.Location.Location.Core

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回位置服务是否可用。 |

**示例**
  
  ```js
  geolocation.disableLocation().then((result) => {
      console.log('promise, disableLocation: ' + JSON.stringify(result));
  });
  ```

## geolocation.isGeoServiceAvailable

isGeoServiceAvailable(callback: AsyncCallback&lt;boolean&gt;) : void

判断（逆）地理编码服务状态，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收地理编码服务状态的回调。 |

**示例**
  
  ```js
  geolocation.isGeoServiceAvailable((err, data) => {
      if (err) {
          console.log('isGeoServiceAvailable: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('isGeoServiceAvailable: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.isGeoServiceAvailable

isGeoServiceAvailable() : Promise&lt;boolean&gt;

判断（逆）地理编码服务状态，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 返回地理编码服务是否可用的状态。 |

**示例**
  
  ```js
  geolocation.isGeoServiceAvailable().then((result) => {
      console.log('promise, isGeoServiceAvailable: ' + JSON.stringify(result));
  });
  ```


## geolocation.getAddressesFromLocation

getAddressesFromLocation(request: ReverseGeoCodeRequest, callback: AsyncCallback&lt;Array&lt;GeoAddress&gt;&gt;) : void

调用逆地理编码服务，将坐标转换为地理描述，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [ReverseGeoCodeRequest](#reversegeocoderequest) | 是 | 设置逆地理编码请求的相关参数。 |
  | callback | AsyncCallback&lt;Array&lt;[GeoAddress](#geoaddress)&gt;&gt; | 是 | 设置接收逆地理编码请求的回调参数。 |

**示例**
  
  ```js
  var reverseGeocodeRequest = {"latitude": 31.12, "longitude": 121.11, "maxItems": 1};
  geolocation.getAddressesFromLocation(reverseGeocodeRequest, (err, data) => {
      if (err) {
          console.log('getAddressesFromLocation: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('getAddressesFromLocation: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.getAddressesFromLocation

getAddressesFromLocation(request: ReverseGeoCodeRequest) : Promise&lt;Array&lt;GeoAddress&gt;&gt;;

调用逆地理编码服务，将坐标转换为地理描述，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [ReverseGeoCodeRequest](#reversegeocoderequest) | 是 | 设置逆地理编码请求的相关参数。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;Array&lt;[GeoAddress](#geoaddress)&gt;&gt; | 返回地理描述信息。 |

**示例**
  
  ```js
  var reverseGeocodeRequest = {"latitude": 31.12, "longitude": 121.11, "maxItems": 1};
  geolocation.getAddressesFromLocation(reverseGeocodeRequest).then((data) => {
      console.log('getAddressesFromLocation: ' + JSON.stringify(data));
  });
  ```


## geolocation.getAddressesFromLocationName

getAddressesFromLocationName(request: GeoCodeRequest, callback: AsyncCallback&lt;Array&lt;GeoAddress&gt;&gt;) : void

调用地理编码服务，将地理描述转换为具体坐标，使用callback回调异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [GeoCodeRequest](#geocoderequest) | 是 | 设置地理编码请求的相关参数。 |
  | callback | AsyncCallback&lt;Array&lt;[GeoAddress](#geoaddress)&gt;&gt; | 是 | 设置接收地理编码请求的回调参数。 |

**示例**
  
  ```js
  var geocodeRequest = {"description": "上海市浦东新区xx路xx号", "maxItems": 1};
  geolocation.getAddressesFromLocationName(geocodeRequest, (err, data) => {
      if (err) {
          console.log('getAddressesFromLocationName: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('getAddressesFromLocationName: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.getAddressesFromLocationName

getAddressesFromLocationName(request: GeoCodeRequest) : Promise&lt;Array&lt;GeoAddress&gt;&gt;

调用地理编码服务，将地理描述转换为具体坐标，使用Promise方式异步返回结果。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | request | [GeoCodeRequest](#geocoderequest) | 是 | 设置地理编码请求的相关参数。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;Array&lt;[GeoAddress](#geoaddress)&gt;&gt; | 设置接收地理编码请求的回调参数。 |

**示例**
  
  ```js
  var geocodeRequest = {"description": "上海市浦东新区xx路xx号", "maxItems": 1};
  geolocation.getAddressesFromLocationName(geocodeRequest).then((result) => {
      console.log('getAddressesFromLocationName: ' + JSON.stringify(result));
  });
  ```


## geolocation.getCachedGnssLocationsSize<sup>8+</sup>

getCachedGnssLocationsSize(callback: AsyncCallback&lt;number&gt;) : void;

获取GNSS芯片缓存位置的个数。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | 是 | 用来接收GNSS芯片缓存位置个数的回调。 |

**示例**
  
  ```js
  geolocation.getCachedGnssLocationsSize((err, size) => {
      if (err) {
          console.log('getCachedGnssLocationsSize: err=' + JSON.stringify(err));
      }
      if (size) {
          console.log('getCachedGnssLocationsSize: size=' + JSON.stringify(size));
      }
  });
  ```


## geolocation.getCachedGnssLocationsSize<sup>8+</sup>

getCachedGnssLocationsSize() : Promise&lt;number&gt;;

获取GNSS芯片缓存位置的个数。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;number&gt; | 返回GNSS缓存位置的个数。 |

**示例**
  
  ```js
  geolocation.getCachedGnssLocationsSize().then((result) => {
      console.log('promise, getCachedGnssLocationsSize: ' + JSON.stringify(result));
  });
  ```


## geolocation.flushCachedGnssLocations<sup>8+</sup>

flushCachedGnssLocations(callback: AsyncCallback&lt;boolean&gt;) : void;

读取并清空GNSS芯片所有缓存位置。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收清空GNSS芯片缓存位置操作的结果。 |

**示例**
  
  ```js
  geolocation.flushCachedGnssLocations((err, result) => {
      if (err) {
          console.log('flushCachedGnssLocations: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('flushCachedGnssLocations: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.flushCachedGnssLocations<sup>8+</sup>

flushCachedGnssLocations() : Promise&lt;boolean&gt;;

读取并清空GNSS芯片所有缓存位置。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 清空所有GNSS缓存位置是否成功。 |

**示例**
  
  ```js
  geolocation.flushCachedGnssLocations().then((result) => {
      console.log('promise, flushCachedGnssLocations: ' + JSON.stringify(result));
  });
  ```


## geolocation.sendCommand<sup>8+</sup>

sendCommand(command: LocationCommand, callback: AsyncCallback&lt;boolean&gt;) : void;

给位置服务子系统的各个部件发送扩展命令。只有系统应用才能调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | command | LocationCommand | 是 | 指定目标场景，和将要发送的命令（字符串）。 |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 用来接收命令发送的结果。 |

**示例**
  
  ```js
  var requestInfo = {'scenario': 0x301, 'command': "command_1"};
  geolocation.sendCommand(requestInfo, (err, result) => {
      if (err) {
          console.log('sendCommand: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('sendCommand: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.sendCommand<sup>8+</sup>

sendCommand(command: LocationCommand) : Promise&lt;boolean&gt;;

给位置服务子系统的各个部件发送扩展命令。只有系统应用才能调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | command | LocationCommand | 是 | 指定目标场景，和将要发送的命令（字符串）。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 表示命令发送成功或失败。 |

**示例**
  
  ```js
  var requestInfo = {'scenario': 0x301, 'command': "command_1"};
  geolocation.sendCommand(requestInfo).then((result) => {
      console.log('promise, sendCommand: ' + JSON.stringify(result));
  });
  ```


## geolocation.isLocationPrivacyConfirmed<sup>8+</sup>

isLocationPrivacyConfirmed(type : LocationPrivacyType, callback: AsyncCallback&lt;boolean&gt;) : void;

查询用户是否同意定位服务隐私申明，是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | LocationPrivacyType | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 表示用户是否同意定位服务隐私申明。 |

**示例**
  
  ```js
  geolocation.isLocationPrivacyConfirmed(1, (err, result) => {
      if (err) {
          console.log('isLocationPrivacyConfirmed: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('isLocationPrivacyConfirmed: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.isLocationPrivacyConfirmed<sup>8+</sup>

isLocationPrivacyConfirmed(type : LocationPrivacyType,) : Promise&lt;boolean&gt;;

查询用户是否同意定位服务隐私申明，是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | LocationPrivacyType | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 表示用户是否同意定位服务隐私申明。 |

**示例**
  
  ```js
  geolocation.isLocationPrivacyConfirmed(1).then((result) => {
      console.log('promise, isLocationPrivacyConfirmed: ' + JSON.stringify(result));
  });
  ```


## geolocation.setLocationPrivacyConfirmStatus<sup>8+</sup>

setLocationPrivacyConfirmStatus(type : LocationPrivacyType, isConfirmed: boolean, callback: AsyncCallback&lt;boolean&gt;) : void;

设置用户勾选定位服务隐私申明的状态，记录用户是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | LocationPrivacyType | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |
  | isConfirmed | boolean | 是 | 表示用户是否同意定位服务隐私申明。 |
  | callback | AsyncCallback&lt;boolean&gt; | 是 | 表示操作是否成功。 |

**示例**
  
  ```js
  geolocation.setLocationPrivacyConfirmStatus(1, true, (err, result) => {
      if (err) {
          console.log('setLocationPrivacyConfirmStatus: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('setLocationPrivacyConfirmStatus: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.setLocationPrivacyConfirmStatus<sup>8+</sup>

setLocationPrivacyConfirmStatus(type : LocationPrivacyType, isConfirmed : boolean) : Promise&lt;boolean&gt;;

设置用户勾选定位服务隐私申明的状态，记录用户是否同意启用定位服务。只有系统应用才能调用。

**系统API**：此接口为系统接口，三方应用不支持调用。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | type | LocationPrivacyType | 是 | 指定隐私申明场景，例如开机向导中的隐私申明、开启网络定位功能时弹出的隐私申明等。 |
  | isConfirmed | boolean | 是 | 表示用户是否同意定位服务隐私申明。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;boolean&gt; | 表示操作是否成功。 |

**示例**
  
  ```js
  geolocation.setLocationPrivacyConfirmStatus(1, true).then((result) => {
      console.log('promise, setLocationPrivacyConfirmStatus: ' + JSON.stringify(result));
  });
  ```


## geolocation.getCountryCode<sup>9+</sup>

getCountryCode(callback: AsyncCallback&lt;CountryCode&gt;) : void;

查询当前的国家码。

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;CountryCode&gt; | 是 | 用来接收国家码。 |

**示例**
  
  ```js
  geolocation.getCountryCode((err, result) => {
      if (err) {
          console.log('getCountryCode: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('getCountryCode: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.getCountryCode<sup>9+</sup>

getCountryCode() : Promise&lt;CountryCode&gt;;

查询当前的国家码。

**系统能力**：SystemCapability.Location.Location.Core

**参数**：

无

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;CountryCode&gt; | 返回国家码。 |

**示例**
  
  ```js
  geolocation.getCountryCode()
  .then((result) => {
      console.log('promise, getCountryCode: result=' + JSON.stringify(result));
  })
  .catch((error) => {
      console.log('promise, getCountryCode: error=' + JSON.stringify(error));
  });
  ```


## geolocation.enableLocationMock<sup>9+</sup>

enableLocationMock(scenario?: LocationRequestScenario, callback: AsyncCallback&lt;void&gt;) : void;

使能某个场景的位置模拟功能，同一时间只能使能一个场景的位置模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | scenario | LocationRequestScenario | 否 | 指示在什么场景下使能位置模拟功能。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。 |

**示例**
  
  ```js
  var request = {"scenario": 0x0301};
  geolocation.enableLocationMock(request, (err, result) => {
      if (err) {
          console.log('enableLocationMock: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('enableLocationMock: result=' + JSON.stringify(result));
      }
  });
  ```

## geolocation.enableLocationMock<sup>9+</sup>

enableLocationMock(scenario?: LocationRequestScenario) : Promise&lt;void&gt;;

使能某个场景的位置模拟功能，同一时间只能使能一个场景的位置模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | scenario | LocationRequestScenario | 否 | 指示使能什么场景的位置模拟功能。如果不携带该参数则表示使能所有场景的位置模拟功能。 |


**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。  |

**示例**
  
  ```js
  var request = {"scenario": 0x0301};
  geolocation.enableLocationMock(request)
  .then((result) => {
      if (result) {
        console.log('promise, enableLocationMock: result=' + JSON.stringify(result));
      }
  })
  .catch((error) => {
      if (error) {
        console.log('promise, enableLocationMock: error=' + JSON.stringify(error));
      }
  });
  ```


## geolocation.disableLocationMock<sup>9+</sup>

disableLocationMock(scenario?: LocationRequestScenario, callback: AsyncCallback&lt;void&gt;) : void;

去使能位置模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | scenario | LocationRequestScenario | 否 | 指示去使能某个场景的位置模拟功能。如果不携带该参数则表示去使能所有场景的位置模拟功能。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。 |

**示例**
  
  ```js
  var request = {"scenario": 0x0301};
  geolocation.disableLocationMock(request, (err, result) => {
      if (err) {
          console.log('disableLocationMock: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('disableLocationMock: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.disableLocationMock<sup>9+</sup>

disableLocationMock(scenario?: LocationRequestScenario) : Promise&lt;void&gt;;

去使能位置模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | scenario | LocationRequestScenario | 否 | 指示去使能某个场景的位置模拟功能。如果不携带该参数则表示去使能所有场景的位置模拟功能。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。  |

**示例**
  
  ```js
  var request = {"scenario": 0x0301};
  geolocation.disableLocationMock(request)
  .then((result) => {
      if (result) {
        console.log('promise, disableLocationMock: result=' + JSON.stringify(result));
      }
  })
  .catch((error) => {
      if (error) {
        console.log('promise, disableLocationMock: error=' + JSON.stringify(error));
      }
  });
  ```


## geolocation.setMockedLocations<sup>9+</sup>

setMockedLocations(config: LocationMockConfig, callback: AsyncCallback&lt;void&gt;) : void;

设置模拟的位置信息，后面会以该接口中携带的时间间隔上报模拟位置。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | config | LocationMockConfig | 是 | 指示位置模拟的配置参数，包含模拟位置上报的时间间隔和模拟位置数组。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。 |

**示例**
  
  ```js
  var locations = [
      {"latitude": 30.12, "longitude": 120.11, "altitude": 123, "accuracy": 1, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 1000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 31.13, "longitude": 121.11, "altitude": 123, "accuracy": 2, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 2000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 32.14, "longitude": 122.11, "altitude": 123, "accuracy": 3, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 3000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 33.15, "longitude": 123.11, "altitude": 123, "accuracy": 4, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 4000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 34.16, "longitude": 124.11, "altitude": 123, "accuracy": 5, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 5000000000, "additionSize": 0, "isFromMock": true}
  ];
  var config = {"timeInterval": 5, "locations": locations};
  geolocation.setMockedLocations(config, (err, data) => {
      if (err) {
          console.log('setMockedLocations: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('setMockedLocations: data=' + JSON.stringify(data));
      }
  });
  ```

## geolocation.setMockedLocations<sup>9+</sup>

setMockedLocations(config: LocationMockConfig) : Promise&lt;void&gt;;

设置模拟的位置信息，后面会以该接口中携带的时间间隔上报模拟位置。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | config | LocationMockConfig | 是 | 指示位置模拟的配置参数，包含模拟位置上报的时间间隔和模拟位置数组。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。  |

**示例**
  
  ```js
  var locations = [
      {"latitude": 30.12, "longitude": 120.11, "altitude": 123, "accuracy": 1, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 1000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 31.13, "longitude": 121.11, "altitude": 123, "accuracy": 2, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 2000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 32.14, "longitude": 122.11, "altitude": 123, "accuracy": 3, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 3000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 33.15, "longitude": 123.11, "altitude": 123, "accuracy": 4, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 4000000000, "additionSize": 0, "isFromMock": true},
      {"latitude": 34.16, "longitude": 124.11, "altitude": 123, "accuracy": 5, "speed": 5.2, "timeStamp": 16594326109, "direction": 123.11, "timeSinceBoot": 5000000000, "additionSize": 0, "isFromMock": true}
  ];
  var config = {"timeInterval": 5, "locations":locations};
  geolocation.setMockedLocations(config)
  .then((result) => {
      if (result) {
        console.log('promise, setMockedLocations: result=' + JSON.stringify(result));
      }
  })
  .catch((error) => {
      if (error) {
        console.log('promise, setMockedLocations: error=' + JSON.stringify(error));
      }
  });
  ```



## geolocation.enableReverseGeocodingMock<sup>9+</sup>

enableReverseGeocodingMock(callback: AsyncCallback&lt;void&gt;) : void;

使能逆地理编码模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | 是 | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。 |

**示例**
  
  ```js
  geolocation.enableReverseGeocodingMock((err, data) => {
      if (err) {
          console.log('enableReverseGeocodingMock: err=' + JSON.stringify(err));
      }
      if (data) {
          console.log('enableReverseGeocodingMock: data=' + JSON.stringify(data));
      }
  });
  ```


## geolocation.enableReverseGeocodingMock<sup>9+</sup>

enableReverseGeocodingMock() : Promise&lt;void&gt;;

使能逆地理编码模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

无

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。  |

**示例**
  
  ```js
  geolocation.enableReverseGeocodingMock()
  .then((result) => {
      if (result) {
        console.log('promise, enableReverseGeocodingMock: result=' + JSON.stringify(result));
      }
  })
  .catch((error) => {
      if (error) {
        console.log('promise, enableReverseGeocodingMock: error=' + JSON.stringify(error));
      }
  });
  ```


## geolocation.disableReverseGeocodingMock<sup>9+</sup>

disableReverseGeocodingMock(callback: AsyncCallback&lt;void&gt;) : void;

去使能逆地理编码模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;void&gt; | 是 | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。 |

**示例**
  
  ```js
  geolocation.disableReverseGeocodingMock((err, result) => {
      if (err) {
          console.log('disableReverseGeocodingMock: err=' + JSON.stringify(err));
      }
      if (result) {
          console.log('disableReverseGeocodingMock: result=' + JSON.stringify(result));
      }
  });
  ```


## geolocation.disableReverseGeocodingMock<sup>9+</sup>

disableReverseGeocodingMock() : Promise&lt;void&gt;;

去使能逆地理编码模拟功能。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

无

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。  |

**示例**
  
  ```js
  geolocation.disableReverseGeocodingMock()
  .then((result) => {
      if (result) {
        console.log('promise, disableReverseGeocodingMock: result=' + JSON.stringify(result));
      }
  })
  .catch((error) => {
      if (error) {
        console.log('promise, disableReverseGeocodingMock: error=' + JSON.stringify(error));
      }
  });
  ```


## geolocation.setReverseGeocodingMockInfo<sup>9+</sup>

setReverseGeocodingMockInfo(mockInfos: Array&lt;ReverseGeocodingMockInfo&gt;, callback: AsyncCallback&lt;void&gt;) : void;

设置逆地理编码模拟功能的配置信息，包含了位置和地名的对应关系，后续进行逆地理编码查询时如果位置信息位于配置信息中，就返回对应的地名。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | mockInfos | Array&lt;ReverseGeocodingMockInfo&gt; | 是 | 指示逆地理编码模拟功能的配置参数数组。逆地理编码模拟功能的配置参数包含了一个位置和一个地名。 |
  | callback | AsyncCallback&lt;void&gt; | 是 | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。 |

**示例**
  
  ```js
  var mockInfos = [
      {"location": {"locale": "zh", "latitude": 30.12, "longitude": 120.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 30.12, "longitude": 120.11, "maxItems": 1, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 31.12, "longitude": 121.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 31.12, "longitude": 121.11, "maxItems": 1, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 32.12, "longitude": 122.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 32.12, "longitude": 122.11, "maxItems": 1, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 33.12, "longitude": 123.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 33.12, "longitude": 123.11, "maxItems": 1, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 34.12, "longitude": 124.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 34.12, "longitude": 124.11, "maxItems": 1, "isFromMock": true}},
  ];
  geolocation.setReverseGeocodingMockInfo(mockInfos, (err, data) => {
      if (err) {
          console.log('promise, setReverseGeocodingMockInfo, err:' + JSON.stringify(err));
      } 
      if (data) {
          console.log('promise, setReverseGeocodingMockInfo, data:' + JSON.stringify(data));
      }
  });
  ```


## geolocation.setReverseGeocodingMockInfo<sup>9+</sup>

setReverseGeocodingMockInfo(mockInfos: Array&lt;ReverseGeocodingMockInfo&gt;) : Promise&lt;void&gt;;

设置逆地理编码模拟功能的配置信息，包含了位置和地名的对应关系，后续进行逆地理编码查询时如果位置信息位于配置信息中，就返回对应的地名。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

**参数**：

  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | mockInfos | Array&lt;ReverseGeocodingMockInfo&gt; | 是 | 指示逆地理编码模拟功能的配置信息数组。逆地理编码模拟功能的配置信息包含了一个位置和一个地名。 |

**返回值**：

  | 参数名 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 用来接收执行结果，如果执行成功就返回nullptr，否则就返回错误信息。  |

**示例**
  
  ```js
  var mockInfos = [
      {"location": {"locale": "zh", "latitude": 30.12, "longitude": 120.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 30.12, "longitude": 120.11, "maxItems": 1, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 31.12, "longitude": 121.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 31.12, "longitude": 121.11, "maxItems": 1, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 32.12, "longitude": 122.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 32.12, "longitude": 122.11, "maxItems": 1, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 33.12, "longitude": 123.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 33.12, "longitude": 123.11, "maxItems": 1, "isFromMock": true}},
      {"location": {"locale": "zh", "latitude": 34.12, "longitude": 124.11, "maxItems": 1}, "geoAddress": {"locale": "zh", "latitude": 34.12, "longitude": 124.11, "maxItems": 1, "isFromMock": true}},
  ];
  geolocation.setReverseGeocodingMockInfo(mockInfos)
  .then((result) => {
      if (result) {
        console.log('promise, setReverseGeocodingMockInfo: result=' + JSON.stringify(result));
      }
  })
  .catch((error) => {
      if (error) {
        console.log('promise, setReverseGeocodingMockInfo: error=' + JSON.stringify(error));
      }
  });
  ```


## LocationRequestPriority

位置请求中位置信息优先级设置。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| UNSET | 0x200 | 表示未设置优先级。 |
| ACCURACY | 0x201 | 表示精度优先。 |
| LOW_POWER | 0x202 | 表示低功耗优先。 |
| FIRST_FIX | 0x203 | 表示快速获取位置优先，如果应用希望快速拿到1个位置，可以将优先级设置为该字段。 |


## LocationRequestScenario

  位置请求中定位场景设置。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| UNSET | 0x300 | 表示未设置场景信息。 |
| NAVIGATION | 0x301 | 表示导航场景。 |
| TRAJECTORY_TRACKING | 0x302 | 表示运动轨迹记录场景。 |
| CAR_HAILING | 0x303 | 表示打车场景。 |
| DAILY_LIFE_SERVICE | 0x304 | 表示日常服务使用场景。 |
| NO_POWER | 0x305 | 表示无功耗功场景，这种场景下不会主动触发定位，会在其他应用定位时，才给当前应用返回位置。 |


## GeoLocationErrorCode

位置服务中的错误码信息。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| NOT_SUPPORTED<sup>9+</sup> | 100 | 表示该接口功能不支持。 |
| INPUT_PARAMS_ERROR<sup>7+</sup> | 101 | 表示输入参数错误。 |
| REVERSE_GEOCODE_ERROR<sup>7+</sup> | 102 | 表示逆地理编码接口调用失败。 |
| GEOCODE_ERROR<sup>7+</sup> | 103 | 表示地理编码接口调用失败。 |
| LOCATOR_ERROR<sup>7+</sup> | 104 | 表示定位失败。 |
| LOCATION_SWITCH_ERROR<sup>7+</sup> | 105 | 表示定位开关。 |
| LAST_KNOWN_LOCATION_ERROR<sup>7+</sup> | 106 | 表示获取上次位置失败。 |
| LOCATION_REQUEST_TIMEOUT_ERROR<sup>7+</sup> | 107 | 表示单次定位，没有在指定时间内返回位置。 |
| QUERY_COUNTRY_CODE_ERROR<sup>9+</sup> | 108 | 表示国家码查询失败。 |


## ReverseGeoCodeRequest

逆地理编码请求接口。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| locale | string | 否 | 指定位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| latitude | number | 是 | 表示纬度信息，正值表示北纬，负值表示南纬。 |
| longitude | number | 是 | 表示经度信息，正值表示东经，负值表示西经。 |
| maxItems | number | 否 | 指定返回位置信息的最大个数。 |


## GeoCodeRequest

地理编码请求接口。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| locale | string | 否 | 表示位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| description | number | 是 | 表示位置信息描述，如“上海市浦东新区xx路xx号”。 |
| maxItems | number | 否 | 表示返回位置信息的最大个数。 |
| minLatitude | number | 否 | 表示最小纬度信息，与下面三个参数一起，表示一个经纬度范围。 |
| minLongitude | number | 否 | 表示最小经度信息。 |
| maxLatitude | number | 否 | 表示最大纬度信息。 |
| maxLongitude | number | 否 | 表示最大经度信息。 |


## GeoAddress

地理编码类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geocoder

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| latitude<sup>7+</sup> | number | 否 | 表示纬度信息，正值表示北纬，负值表示南纬。 |
| longitude<sup>7+</sup> | number | 否 | 表示经度信息，正值表示东经，负值表是西经。 |
| locale<sup>7+</sup> | string | 否 | 表示位置描述信息的语言，“zh”代表中文，“en”代表英文。 |
| placeName<sup>7+</sup> | string | 否 | 表示地区信息。 |
| countryCode<sup>7+</sup> | string | 否 | 表示国家码信息。 |
| countryName<sup>7+</sup> | string | 否 | 表示国家信息。 |
| administrativeArea<sup>7+</sup> | string | 否 | 表示省份区域信息。 |
| subAdministrativeArea<sup>7+</sup> | string | 否 | 表示表示子区域信息。 |
| locality<sup>7+</sup> | string | 否 | 表示城市信息。 |
| subLocality<sup>7+</sup> | string | 否 | 表示子城市信息。 |
| roadName<sup>7+</sup> | string | 否 | 表示路名信息。 |
| subRoadName<sup>7+</sup> | string | 否 | 表示子路名信息。 |
| premises<sup>7+</sup> | string | 否 | 表示门牌号信息。 |
| postalCode<sup>7+</sup> | string | 否 | 表示邮政编码信息。 |
| phoneNumber<sup>7+</sup> | string | 否 | 表示联系方式信息。 |
| addressUrl<sup>7+</sup> | string | 否 | 表示位置信息附件的网址信息。 |
| descriptions<sup>7+</sup> | Array&lt;string&gt; | 否 | 表示附加的描述信息。 |
| descriptionsSize<sup>7+</sup> | number | 否 | 表示附加的描述信息数量。 |
| isFromMock<sup>9+</sup> | Boolean | 否 | 表示地名信息是否来自于逆地理编码模拟功能。 |


## LocationRequest

位置信息请求类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestpriority) | 否 | 表示优先级信息。 |
| scenario | [LocationRequestScenario](#locationrequestscenario) | 是 | 表示场景信息。 |
| timeInterval | number | 否 | 表示上报位置信息的时间间隔。 |
| distanceInterval | number | 否 | 表示上报位置信息的距离间隔。 |
| maxAccuracy | number | 否 | 表示精度信息。 |


## CurrentLocationRequest

当前位置信息请求类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| priority | [LocationRequestPriority](#locationrequestpriority) | 否 | 表示优先级信息。 |
| scenario | [LocationRequestScenario](#locationrequestscenario) | 否 | 表示场景信息。 |
| maxAccuracy | number | 否 | 表示精度信息，单位是米。 |
| timeoutMs | number | 否 | 表示超时时间，单位是毫秒，最小为1000毫秒。 |


## SatelliteStatusInfo<sup>8+</sup>

卫星状态信息。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| satellitesNumber | number | 是 | 表示卫星个数。 |
| satelliteIds | Array&lt;number&gt; | 是 | 表示每个卫星的ID，数组类型。 |
| carrierToNoiseDensitys | Array&lt;number&gt; | 是 | 表示载波噪声功率谱密度比，即cn0。 |
| altitudes | Array&lt;number&gt; | 是 | 表示高程信息。 |
| azimuths | Array&lt;number&gt; | 是 | 表示方位角。 |
| carrierFrequencies | Array&lt;number&gt; | 是 | 表示载波频率。 |


## CachedGnssLocationsRequest<sup>8+</sup>

请求订阅GNSS缓存位置上报功能接口的配置参数。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Gnss

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| reportingPeriodSec | number | 是 | 表示GNSS缓存位置上报的周期，单位是毫秒。 |
| wakeUpCacheQueueFull | boolean | 是 | true表示GNSS芯片底层缓存队列满之后会主动唤醒AP芯片，并把缓存位置上报给应用。<br/>false表示GNSS芯片底层缓存队列满之后不会主动唤醒AP芯片，会把缓存位置直接丢弃。 |


## Geofence<sup>8+</sup>

GNSS围栏的配置参数。目前只支持圆形围栏。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| latitude | number | 是 | 表示纬度。 |
| longitude | number | 是 | 表示经度。 |
| radius | number | 是 | 表示圆形围栏的半径。 |
| expiration | number | 是 | 围栏存活的时间，单位是毫秒。 |


## GeofenceRequest<sup>8+</sup>

请求添加GNSS围栏消息中携带的参数，包括定位优先级、定位场景和围栏信息。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Geofence

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| priority | LocationRequestPriority | 是 | 表示位置信息优先级。 |
| scenario | LocationRequestScenario | 是 | 表示定位场景。 |
| geofence | Geofence | 是 | 表示围栏信息。 |


## LocationPrivacyType<sup>8+</sup>

定位服务隐私协议类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| OTHERS | 0 | 其他场景。 |
| STARTUP | 1 | 开机向导场景下的隐私协议。 |
| CORE_LOCATION | 2 | 开启网络定位时弹出的隐私协议。 |


## LocationCommand<sup>8+</sup>

扩展命令结构体。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| scenario | LocationRequestScenario | 是 | 表示定位场景。 |
| command | string | 是 | 扩展命令字符串。 |


## Location

位置信息类型。

**需要权限**：ohos.permission.LOCATION

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| latitude<sup>7+</sup> | number | 是 | 表示纬度信息，正值表示北纬，负值表示南纬。 |
| longitude<sup>7+</sup> | number | 是 | 表示经度信息，正值表示东经，负值表是西经。 |
| altitude<sup>7+</sup> | number | 是 | 表示高度信息，单位米。 |
| accuracy<sup>7+</sup> | number | 是 | 表示精度信息，单位米。 |
| speed<sup>7+</sup> | number | 是 | 表示速度信息，单位米每秒。 |
| timeStamp<sup>7+</sup> | number | 是 | 表示位置时间戳，UTC格式。 |
| direction<sup>7+</sup> | number | 是 | 表示航向信息。 |
| timeSinceBoot<sup>7+</sup> | number | 是 | 表示位置时间戳，开机时间格式。 |
| additions<sup>7+</sup> | Array&lt;string&gt; | 否 | 附加信息。 |
| additionSize<sup>7+</sup> | number | 否 | 附加信息数量。 |
| isFromMock<sup>9+</sup> | Boolean | 否 | 表示位置信息是否来自于位置模拟功能。 |


## ReverseGeocodingMockInfo<sup>9+</sup>

逆地理编码模拟功能的配置信息，包含一个位置信息和一个地名信息。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| location | ReverseGeoCodeRequest | 是 | 表示经纬度信息。 |
| geoAddress | GeoAddress | 是 | 表示地名信息。 |


## LocationMockConfig<sup>9+</sup>

位置模拟功能的配置参数，包含了模拟位置上报的时间间隔和模拟位置数组。

**系统能力**：SystemCapability.Location.Location.Core

**系统API**：此接口为系统接口，三方应用不支持调用。

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| timeInterval | number | 是 | 表示模拟位置上报的时间间隔，单位是秒。 |
| locations | Array&lt;Location&gt; | 是 | 表示模拟位置数组。 |


## CountryCode<sup>9+</sup>

国家码信息结构体，包含国家码字符串和国家码的来源信息。

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 参数类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| country | string | 是 | 表示国家码字符串。 |
| type | CountryCodeType | 是 | 表示国家码信息来源。 |


## CountryCodeType<sup>9+</sup>

国家码来源类型。

**系统能力**：SystemCapability.Location.Location.Core

| 名称 | 默认值 | 说明 |
| -------- | -------- | -------- |
| COUNTRY_CODE_FROM_LOCALE | 1 | 从全球化模块的语言配置信息中获取到的国家码。 |
| COUNTRY_CODE_FROM_SIM | 2 | 从SIM卡中获取到的国家码。 |
| COUNTRY_CODE_FROM_LOCATION | 3 | 基于用户的位置信息，通过逆地理编码查询到的国家码。 |
| COUNTRY_CODE_FROM_NETWORK | 4 | 从蜂窝网络注册信息中获取到的国家码。 |