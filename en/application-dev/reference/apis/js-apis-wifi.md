# WLAN
The WLAN module provides basic wireless local area network (WLAN) functions, peer-to-peer (P2P) functions, and WLAN message notification services. It allows applications to communicate with other devices over WLAN.

> **NOTE**<br>
> The initial APIs of this module are supported since API version 6. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```js
import wifi from '@ohos.wifi';
```

## wifi.enableWifi

enableWifi(): boolean

Enables WLAN.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.disableWifi

disableWifi(): boolean

Disables WLAN.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.isWifiActive

isWifiActive(): boolean

Checks whether WLAN is enabled.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if WLAN is enabled; returns **false** otherwise.|


## wifi.scan

scan(): boolean

Starts a scan for WLAN.

**Required permissions**: **ohos.permission.SET_WIFI_INFO** and **ohos.permission.LOCATION**

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.getScanInfos

getScanInfos(): Promise&lt;Array&lt;WifiScanInfo&gt;&gt;

Obtains the scan result. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_PEERS_MAC (or ohos.permission.LOCATION)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | Promise&lt;&nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo)&gt;&nbsp;&gt; | Promise used to return the detected hotspots.|


## wifi.getScanInfos

getScanInfos(callback: AsyncCallback&lt;Array&lt;WifiScanInfo&gt;&gt;): void

Obtains the scan result. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_PEERS_MAC (or ohos.permission.LOCATION)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;&nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo)&gt;&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the detected hotspots. Otherwise, **err** is a non-zero value and **data** is empty.|

**Example**
  ```js
  import wifi from '@ohos.wifi';
  
  wifi.getScanInfos((err, result) => {
      if (err) {
          console.error("get scan info error");
          return;
      }
  
      var len = Object.keys(result).length;
      console.log("wifi received scan info: " + len);
      for (var i = 0; i < len; ++i) {
          console.info("ssid: " + result[i].ssid);
          console.info("bssid: " + result[i].bssid);
          console.info("capabilities: " + result[i].capabilities);
          console.info("securityType: " + result[i].securityType);
          console.info("rssi: " + result[i].rssi);
          console.info("band: " + result[i].band);
          console.info("frequency: " + result[i].frequency);
          console.info("channelWidth: " + result[i].channelWidth);
          console.info("timestamp: " + result[i].timestamp);
      }
  });
  
  wifi.getScanInfos().then(result => {
      var len = Object.keys(result).length;
      console.log("wifi received scan info: " + len);
      for (var i = 0; i < len; ++i) {
          console.info("ssid: " + result[i].ssid);
          console.info("bssid: " + result[i].bssid);
          console.info("capabilities: " + result[i].capabilities);
          console.info("securityType: " + result[i].securityType);
          console.info("rssi: " + result[i].rssi);
          console.info("band: " + result[i].band);
          console.info("frequency: " + result[i].frequency);
          console.info("channelWidth: " + result[i].channelWidth);
          console.info("timestamp: " + result[i].timestamp);
      }
  });
  ```


## WifiScanInfo

Represents WLAN hotspot information.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable/Writable**| **Description**|
| -------- | -------- | -------- | -------- |
| ssid | string | Read only| Hotspot service set identifier (SSID), in UTF-8 format.|
| bssid | string | Read only| Basic service set identifier (BSSID) of the hotspot.|
| capabilities | string | Read only| Hotspot capabilities.|
| securityType | [WifiSecurityType](#wifisecuritytype) | Read only| WLAN security type.|
| rssi | number | Read only| Received signal strength indicator (RSSI) of the hotspot, in dBm.|
| band | number | Read only| Frequency band of the WLAN access point (AP).|
| frequency | number | Read only| Frequency of the WLAN AP.|
| channelWidth | number | Read only| Channel width of the WLAN AP.|
| centerFrequency0<sup>9+</sup> | number | Read only| Center frequency.|
| centerFrequency1<sup>9+</sup> | number | Read only| Center frequency.|
| infoElems<sup>9+</sup> | Array&lt;[WifiInfoElem](#wifiinfoelem9)&gt; | Read only| Information elements.|
| timestamp | number | Read only| Timestamp.|


## WifiSecurityType

Enumerates the WLAN security types.

**System capability**: SystemCapability.Communication.WiFi.Core

| **Name**| **Default Value**| **Description**|
| -------- | -------- | -------- |
| WIFI_SEC_TYPE_INVALID | 0 | Invalid security type.|
| WIFI_SEC_TYPE_OPEN | 1 | Open security type.|
| WIFI_SEC_TYPE_WEP | 2 | Wired Equivalent Privacy (WEP).|
| WIFI_SEC_TYPE_PSK | 3 | Pre-shared key (PSK).|
| WIFI_SEC_TYPE_SAE | 4 | Simultaneous Authentication of Equals (SAE).|
| WIFI_SEC_TYPE_EAP<sup>9+</sup> | 5 | Extensible Authentication protocol (EAP).|
| WIFI_SEC_TYPE_EAP_SUITE_B<sup>9+</sup> | 6 | Suite B 192-bit encryption.|
| WIFI_SEC_TYPE_OWE<sup>9+</sup> | 7 | Opportunistic Wireless Encryption (OWE).|
| WIFI_SEC_TYPE_WAPI_CERT<sup>9+</sup> | 8 | WLAN Authentication and Privacy Infrastructure (WAPI) in certificate-based mode (WAPI-CERT).|
| WIFI_SEC_TYPE_WAPI_PSK<sup>9+</sup> | 9 | WAPI-PSK.|


## WifiInfoElem<sup>9+</sup>

Represents a WLAN information element.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable/Writable**| **Description**|
| -------- | -------- | -------- | -------- |
| eid | number | Read only| ID of the information element.|
| content | Uint8Array | Read only| Content of the information element.|


## WifiChannelWidth<sup>9+</sup>

Enumerates the Wi-Fi channel widths.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Default Value**| **Description**|
| -------- | -------- | -------- |
| WIDTH_20MHZ | 0 | 20 MHz.|
| WIDTH_40MHZ | 1 | 40 MHz.|
| WIDTH_80MHZ | 2 | 80 MHz.|
| WIDTH_160MHZ | 3 | 160 MHz.|
| WIDTH_80MHZ_PLUS | 4 | 80 MHz<sup>+</sup>.|
| WIDTH_INVALID | 5 | Invalid value.|


## wifi.getScanInfosSync<sup>9+</sup>

getScanInfosSync(): &nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo)&gt;

Obtains the scan result. This API returns the result synchronously.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_PEERS_MAC (or ohos.permission.LOCATION)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | &nbsp;Array&lt;[WifiScanInfo](#wifiscaninfo)&gt; | Scan result obtained.|


## wifi.addDeviceConfig

addDeviceConfig(config: WifiDeviceConfig): Promise&lt;number&gt;

Adds network configuration. This API uses a promise to return the result.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.SET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to add.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | Promise&lt;number&gt; | Promise used to return the WLAN configuration ID. If **-1** is returned, the operation has failed.|

## WifiDeviceConfig

Represents the WLAN configuration.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable/Writable**| **Description**|
| -------- | -------- | -------- | -------- |
| ssid | string | Read only| SSID of the hotspot, in UTF-8 format.|
| bssid | string | Read only| BSSID of the hotspot.|
| preSharedKey | string | Read only| PSK of the hotspot.|
| isHiddenSsid | boolean | Read only| Whether to hide the network.|
| securityType | [WifiSecurityType](#wifisecuritytype) | Read only| Security type.|
| creatorUid | number | Read only| User ID, which is available only to system applications.|
| disableReason | number | Read only| Reason for disabling WLAN. This parameter is available only to system applications.|
| netId | number | Read only| Allocated network ID, which is available only to system applications.|
| randomMacType | number | Read only| Random MAC type, which is available only to system applications.|
| randomMacAddr | string | Read only| Random MAC address, which is available only for system applications.|
| ipType | [IpType](#iptype7) | Read only| IP address type, which is available only to system applications.|
| staticIp | [IpConfig](#ipconfig7) | Read only| Static IP address configuration, which is available only to system applications.|
| eapConfig<sup>9+</sup> | [WifiEapConfig](#wifieapconfig9) | Read only| EAP configuration, which is available only to system applications.|


## IpType<sup>7+</sup>

Enumerate the IP address types.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Default Value| Description|
| -------- | -------- | -------- |
| STATIC | 0 | Static IP address.|
| DHCP | 1 | IP address allocated by DHCP.|
| UNKNOWN | 2 | Not specified.|


## IpConfig<sup>7+</sup>

Represents IP configuration information.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable/Writable**| **Description**|
| -------- | -------- | -------- | -------- |
| ipAddress | number | Read only| IP address.|
| gateway | number | Read only| Gateway.|
| dnsServers | number[] | Read only| Domain name server (DNS) information.|
| domains | Array&lt;string&gt; | Read only| Domain information.|


## WifiEapConfig<sup>9+</sup>

Represents EAP configuration information.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable/Writable**| **Description**|
| -------- | -------- | -------- | -------- |
| eapMethod | [EapMethod](#eapmethod9) | Read only| EAP authentication method.|
| phase2Method | [Phase2Method](#phase2method9) | Read only| Phase 2 authentication method.|
| identity | string | Read only| Identity Information.|
| anonymousIdentity | string | Read only| Anonymous identity.|
| password | string | Read only| Password.|
| caCertAliases | string | Read only| CA certificate alias.|
| caPath | string | Read only| CA certificate path.|
| clientCertAliases | string | Read only| Client certificate alias.|
| altSubjectMatch | string | Read only| A string to match the alternate subject.|
| domainSuffixMatch | string | Read only| A string to match the domain suffix.|
| realm | string | Read only| Realm for the passpoint credential.|
| plmn | string | Read only| Public land mobile network (PLMN) of the passpoint credential provider.|
| eapSubId | number | Read only| Sub-ID of the SIM card.|


## EapMethod<sup>9+</sup>

Enumerates the EAP authentication methods.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Default Value| Description|
| -------- | -------- | -------- |
| EAP_NONE | 0 | Not specified.|
| EAP_PEAP | 1 | PEAP.|
| EAP_TLS | 2 | TLS.|
| EAP_TTLS | 3 | TTLS.|
| EAP_PWD | 4 | Password.|
| EAP_SIM | 5 | SIM.|
| EAP_AKA | 6 | AKA.|
| EAP_AKA_PRIME | 7 | AKA Prime.|
| EAP_UNAUTH_TLS | 8 | UNAUTH TLS.|


## Phase2Method<sup>9+</sup>

Enumerates the Phase 2 authentication methods.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Default Value| Description|
| -------- | -------- | -------- |
| PHASE2_NONE | 0 | Not specified.|
| PHASE2_PAP | 1 | PAP.|
| PHASE2_MSCHAP | 2 | MS-CHAP.|
| PHASE2_MSCHAPV2 | 3 | MS-CHAPv2.|
| PHASE2_GTC | 4 | GTC .|
| PHASE2_SIM | 5 | SIM.|
| PHASE2_AKA | 6 | AKA.|
| PHASE2_AKA_PRIME | 7 | AKA Prime.|


## wifi.addDeviceConfig

addDeviceConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;number&gt;): void

Adds network configuration. This API uses an asynchronous callback to return the result.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.SET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to add.|
  | callback | AsyncCallback&lt;number&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the network configuration ID. If **data** is **-1**, the operation has failed. If **err** is not **0**, an error has occurred.|


## wifi.addUntrustedConfig<sup>7+</sup>

addUntrustedConfig(config: WifiDeviceConfig): Promise&lt;boolean&gt;

Adds the configuration of an untrusted network. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to add.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result. If the operation is successful, **true** is returned; otherwise, **false** is returned.|


## wifi.addUntrustedConfig<sup>7+</sup>

addUntrustedConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;boolean&gt;): void

Adds the configuration of an untrusted network. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to add.|
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is **true**. If the operation fails, **data** is **false**. If **err** is not **0**, an error has occurred.|


## wifi.removeUntrustedConfig<sup>7+</sup>

removeUntrustedConfig(config: WifiDeviceConfig): Promise&lt;boolean&gt;

Removes the configuration of an untrusted network. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to remove.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result. If the operation is successful, **true** is returned; otherwise, **false** is returned.|


## wifi.removeUntrustedConfig<sup>7+</sup>

removeUntrustedConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;boolean&gt;): void

Removes the configuration of an untrusted network. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to remove.|
  | callback | AsyncCallback&lt;boolean&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is **true**. If the operation fails, **data** is **false**. If **err** is not **0**, an error has occurred.|


## wifi.addCandidateConfig<sup>9+</sup>

addCandidateConfig(config: WifiDeviceConfig): Promise&lt;number&gt;

Adds the configuration of a candidate network. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to add.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | Promise&lt;number&gt; | Promise used to return the network configuration ID.|


## wifi.addCandidateConfig<sup>9+</sup>

addCandidateConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;number&gt;): void

Adds the configuration of a candidate network. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to add.|
  | callback | AsyncCallback&lt;number&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the network configuration ID. If **data** is **-1**, the operation has failed. If **err** is not **0**, an error has occurred.|


## wifi.removeCandidateConfig<sup>9+</sup>

removeCandidateConfig(config: WifiDeviceConfig): Promise&lt;boolean&gt;

Removes the configuration of a candidate network. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to remove.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | Promise&lt;void&gt; | Promise used to return the result. If the operation is successful, **true** is returned; otherwise, **false** is returned.|


## wifi.removeCandidateConfig<sup>9+</sup>

removeCandidateConfig(config: WifiDeviceConfig, callback: AsyncCallback&lt;boolean&gt;): void

Removes the configuration of a candidate network. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration to remove.|
  | callback | AsyncCallback&lt;void&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is **true**. If the operation fails, **data** is **false**. If **err** is not **0**, an error has occurred.|


## wifi.getCandidateConfigs<sup>9+</sup>

getCandidateConfigs(): &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig)&gt;

Obtains candidate network configuration.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig)&gt; | Candidate network configuration obtained.|


## wifi.connectToCandidateConfig<sup>9+</sup>

connectToCandidateConfig(networkId: number): boolean

Connects to a candidate network.

**Required permissions**: ohos.permission.SET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | networkId | number | Yes| ID of the candidate network configuration.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.connectToNetwork

connectToNetwork(networkId: number): boolean

Connects to the specified network.
This is a system API.

**Required permissions**: ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | networkId | number | Yes| Network configuration ID.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.connectToDevice

connectToDevice(config: WifiDeviceConfig): boolean

Connects to the specified network.
This is a system API.

**Required permissions**:
  ohos.permission.SET_WIFI_INFO, ohos.permission.SET_WIFI_CONFIG, and ohos.permissio.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**:
  SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| WLAN configuration.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.disconnect

disconnect(): boolean

Connects to the specified network.
This is a system API.

**Required permissions**:
  ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**:
  SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.getSignalLevel

getSignalLevel(rssi: number, band: number): number

Obtains the WLAN signal level.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | rssi | number | Yes| RSSI of the hotspot, in dBm.|
  | band | number | Yes| Frequency band of the WLAN AP.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | number | Signal level obtained. The value range is [0, 4].|


## wifi.getLinkedInfo

getLinkedInfo(): Promise&lt;WifiLinkedInfo&gt;

Obtains WLAN connection information. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[WifiLinkedInfo](#wifilinkedinfo)&gt; | Promise used to return the WLAN connection information obtained.|


## wifi.getLinkedInfo

getLinkedInfo(callback: AsyncCallback&lt;WifiLinkedInfo&gt;): void

Obtains WLAN connection information. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[WifiLinkedInfo](#wifilinkedinfo)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the WLAN connection information obtained. If **err** is not **0**, an error has occurred.|

**Example**
  ```js
  import wifi from '@ohos.wifi';
  
  wifi.getLinkedInfo((err, data) => {
      if (err) {
          console.error("get linked info error");
          return;
      }
      console.info("get wifi linked info: " + JSON.stringify(data));
  });
  
  wifi.getLinkedInfo().then(data => {
      console.info("get wifi linked info: " + JSON.stringify(data));
  }).catch(error => {
      console.info("get linked info error");
  });
  ```


## WifiLinkedInfo

Represents the WLAN connection information.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Type| Readable/Writable| Description|
| -------- | -------- | -------- | -------- |
| ssid | string | Read only| SSID, in UTF-8 format.|
| bssid | string | Read only| BSSID of the hotspot.|
| networkId | number | Read only| Network configuration ID, which is available only to system applications.|
| rssi | number | Read only| RSSI of the hotspot, in dBm.|
| band | number | Read only| Frequency band of the WLAN AP.|
| linkSpeed | number | Read only| Speed of the WLAN AP.|
| frequency | number | Read only| Frequency of the WLAN AP.|
| isHidden | boolean | Read only| Whether to hide the WLAN AP.|
| isRestricted | boolean | Read only| Whether to restrict data volume at the WLAN AP.|
| chload | number | Read only| Channel load. A larger value indicates a higher load. This parameter is only available to system applications.|
| snr | number | Read only| Signal-to-noise ratio (SNR), which is available only to system applications.|
| macType<sup>9+</sup> | number | Read only| MAC address type.|
| macAddress | string | Read only| MAC address of the device.|
| ipAddress | number | Read only| IP address of the device that sets up the WLAN connection.|
| suppState | [SuppState](#suppstate) | Read only| Supplicant state, which is available only to system applications.|
| connState | [ConnState](#connstate) | Read only| WLAN connection state.|


## ConnState

Enumerates the WLAN connection states.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Default Value| Description|
| -------- | -------- | -------- |
| SCANNING | 0 | The device is scanning for available APs.|
| CONNECTING | 1 | A WLAN connection is being established.|
| AUTHENTICATING | 2 | An authentication is being performed for a WLAN connection.|
| OBTAINING_IPADDR | 3 | The IP address of the WLAN connection is being acquired.|
| CONNECTED | 4 | A WLAN connection is established.|
| DISCONNECTING | 5 | The WLAN connection is being disconnected.|
| DISCONNECTED | 6 | The WLAN connection is disconnected.|
| UNKNOWN | 7 | Failed to set up a WLAN connection.|


## SuppState

Enumerates the supplicant states.

**System capability**: SystemCapability.Communication.WiFi.STA

| Name| Default Value| Description|
| -------- | -------- | -------- |
| DISCONNECTED | 0 | The supplicant is disconnected from the AP.|
| INTERFACE_DISABLED | 1 | The network interface is disabled.|
| INACTIVE | 2 | The supplicant is inactive.|
| SCANNING | 3 | The supplicant is scanning for a WLAN connection.|
| AUTHENTICATING | 4 | The supplicant is being authenticated.|
| ASSOCIATING | 5 | The supplicant is being associated with an AP.|
| ASSOCIATED | 6 | The supplicant is associated with an AP.|
| FOUR_WAY_HANDSHAKE | 7 | A four-way handshake is being performed for the supplicant.|
| GROUP_HANDSHAKE | 8 | A group handshake is being performed for the supplicant.|
| COMPLETED | 9 | The authentication is complete.|
| UNINITIALIZED | 10 | The supplicant failed to set up a connection.|
| INVALID | 11 | Invalid value.|


## wifi.isConnected<sup>7+</sup>

isConnected(): boolean

Checks whether the WLAN is connected.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the WLAN is connected; returns **false** otherwise.|


## wifi.getSupportedFeatures<sup>7+</sup>

getSupportedFeatures(): number

Obtains the features supported by this device.
This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.Core

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | number | Feature value.|

**Feature IDs**

| Value| Description|
| -------- | -------- |
| 0x0001 | WLAN infrastructure mode|
| 0x0002 | 5 GHz feature|
| 0x0004 | Generic Advertisement Service (GAS)/Access Network Query Protocol (ANQP) feature|
| 0x0008 | Wi-Fi Direct|
| 0x0010 | SoftAP|
| 0x0040 | Wi-Fi AWare|
| 0x8000 | WLAN AP/STA concurrency|
| 0x8000000 | WPA3 Personal (WPA-3 SAE)|
| 0x10000000 | WPA3-Enterprise Suite B |
| 0x20000000 | Enhanced open feature|


## wifi.isFeatureSupported<sup>7+</sup>

isFeatureSupported(featureId: number): boolean

Checks whether the device supports the specified WLAN feature.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.Core

**Parameters**

  | **Name**| **Type**| Mandatory| **Description**|
  | -------- | -------- | -------- | -------- |
  | featureId | number | Yes| Feature ID.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the feature is supported; returns **false** otherwise.|


## wifi.getDeviceMacAddress<sup>7+</sup>

getDeviceMacAddress(): string[]

Obtains the device MAC address.
This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_LOCAL_MAC and ohos.permission.GET_WIFI_INFO (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | string[] | MAC address obtained.|


## wifi.getIpInfo<sup>7+</sup>

getIpInfo(): IpInfo

Obtains IP information.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | [IpInfo](#ipinfo7) | IP information obtained.|


## IpInfo<sup>7+</sup>

Represents IP information.

**System capability**: SystemCapability.Communication.WiFi.STA

| **Name**| **Type**| **Readable/Writable**| **Description**|
| -------- | -------- | -------- | -------- |
| ipAddress | number | Read only| IP address.|
| gateway | number | Read only| Gateway.|
| netmask | number | Read only| Subnet mask.|
| primaryDns | number | Read only| IP address of the preferred DNS server.|
| secondDns | number | Read only| IP address of the alternate DNS server.|
| serverIp | number | Read only| IP address of the DHCP server.|
| leaseDuration | number | Read only| Lease duration of the IP address.|


## wifi.getCountryCode<sup>7+</sup>

getCountryCode(): string

Obtains the country code.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.Core

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | string | Country code obtained.|


## wifi.reassociate<sup>7+</sup>

reassociate(): boolean

Re-associates with the network.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.reconnect<sup>7+</sup>

reconnect(): boolean

Reconnects to the network.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.getDeviceConfigs<sup>7+</sup>

getDeviceConfigs(): &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig)&gt;

Obtains network configuration.
This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO, ohos.permission.LOCATION, and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | &nbsp;Array&lt;[WifiDeviceConfig](#wifideviceconfig)&gt; | Array of network configuration obtained.|


## wifi.updateNetwork<sup>7+</sup>

updateNetwork(config: WifiDeviceConfig): boolean

Updates network configuration.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.SET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiDeviceConfig](#wifideviceconfig) | Yes| New WLAN configuration.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.disableNetwork<sup>7+</sup>

disableNetwork(netId: number): boolean

Disables network configuration.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | netId | number | Yes| ID of the network configuration to disable.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.removeAllNetwork<sup>7+</sup>

removeAllNetwork(): boolean

Removes the configuration of all networks.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.removeDevice<sup>7+</sup>

removeDevice(id: number): boolean

Removes the configuration of a network.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | id | number | Yes| ID of the network configuration to remove.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.enableHotspot<sup>7+</sup>

enableHotspot(): boolean

Enables this hotspot.
This is a system API.

**Required permissions**: ohos.permission.MANAGE_WIFI_HOTSPOT (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.disableHotspot<sup>7+</sup>

disableHotspot(): boolean

Disables this hotspot.
This is a system API.

**Required permissions**: ohos.permission.MANAGE_WIFI_HOTSPOT (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.isHotspotDualBandSupported<sup>7+</sup>

isHotspotDualBandSupported(): boolean

Checks whether the hotspot supports dual band.
This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.MANAGE_WIFI_HOTSPOT (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the feature is supported; returns **false** otherwise.|


## wifi.isHotspotActive<sup>7+</sup>

isHotspotActive(): boolean

Checks whether this hotspot is active.
This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the hotspot is active; returns **false** otherwise.|


## wifi.setHotspotConfig<sup>7+</sup>

setHotspotConfig(config: HotspotConfig): boolean

Sets hotspot configuration.
This is a system API.

**Required permissions**: ohos.permission.SET_WIFI_INFO and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [HotspotConfig](#hotspotconfig7) | Yes| Hotspot configuration to set.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## HotspotConfig<sup>7+</sup>

Represents the hotspot configuration.

**System capability**: SystemCapability.Communication.WiFi.AP.Core

| **Name**| **Type**| **Readable/Writable**| **Description**|
| -------- | -------- | -------- | -------- |
| ssid | string | Read only| SSID, in UTF-8 format.|
| securityType | [WifiSecurityType](#wifisecuritytype) | Read only| Security type.|
| band | number | Read only| Hotspot band. The value **1** stands for 2.4 GHz, the value **2** for 5 GHz, and the value **3** for dual band.|
| preSharedKey | string | Read only| SPK of the hotspot.|
| maxConn | number | Read only| Maximum number of connections allowed.|


## wifi.getHotspotConfig<sup>7+</sup>

getHotspotConfig(): HotspotConfig

obtains hotspot configuration.
This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | [HotspotConfig](#hotspotconfig7) | Hotspot configuration obtained.|


## wifi.getStations<sup>7+</sup>

getStations(): &nbsp;Array&lt;[StationInfo](#stationinfo7)&gt;

Obtains information about the connected stations.
This is a system API.

**Required permissions**: ohos.permission.GET_WIFI_INFO, ohos.permission.LOCATION, and ohos.permission.MANAGE_WIFI_HOTSPOT (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | &nbsp;Array&lt;[StationInfo](#stationinfo7)&gt; | Connected stations obtained.|


## StationInfo<sup>7+</sup>

Represents the station information.

**System capability**: SystemCapability.Communication.WiFi.AP.Core

| **Name**| **Type**| **Readable/Writable**| **Description**|
| -------- | -------- | -------- | -------- |
| name | string | Read only| Device name.|
| macAddress | string | Read only| MAC address.|
| ipAddress | string | Read only| IP address.|


## wifi.getP2pLinkedInfo<sup>8+</sup>

getP2pLinkedInfo(): Promise&lt;WifiP2pLinkedInfo&gt;

Obtains P2P link information. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo8)&gt; | Promise used to return the P2P link information obtained.|



## WifiP2pLinkedInfo<sup>8+</sup>

Represents the P2P link information.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Type| Readable/Writable| Description|
| -------- | -------- | -------- | -------- |
| connectState | [P2pConnectState](#p2pconnectstate8) | Read only| P2P connection state.|
| isGroupOwner | boolean | Read only| Whether the device is the group owner.|
| groupOwnerAddr | string | Read only| MAC address of the group.


## P2pConnectState<sup>8+</sup>

Enumerates the P2P connection states.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Default Value| Description|
| -------- | -------- | -------- |
| DISCONNECTED | 0 | Disconnected.|
| CONNECTED | 1 | Connected.|


## wifi.getP2pLinkedInfo<sup>8+</sup>

getP2pLinkedInfo(callback: AsyncCallback&lt;WifiP2pLinkedInfo&gt;): void

Obtains P2P link information. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo8)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the P2P link information. If **err** is not **0**, an error has occurred.|


## wifi.getCurrentGroup<sup>8+</sup>

getCurrentGroup(): Promise&lt;WifiP2pGroupInfo&gt;

Obtains the current P2P group information. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo8)&gt; | Promise used to return the group information obtained.|


## wifi.getCurrentGroup<sup>8+</sup>

getCurrentGroup(callback: AsyncCallback&lt;WifiP2pGroupInfo&gt;): void

Obtains the current P2P group information. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo8)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the group information obtained. If **err** is not **0**, an error has occurred.|


## wifi.getP2pPeerDevices<sup>8+</sup>

getP2pPeerDevices(): Promise&lt;WifiP2pDevice[]&gt;

Obtains the peer device list in a P2P connection. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[WifiP2pDevice[]](#wifip2pdevice8)&gt; | Promise used to return the peer device list.|


## wifi.getP2pPeerDevices<sup>8+</sup>

getP2pPeerDevices(callback: AsyncCallback&lt;WifiP2pDevice[]&gt;): void

Obtains the peer device list in a P2P connection. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[WifiP2pDevice[]](#wifip2pdevice8)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the peer device list obtained. If **err** is not **0**, an error has occurred.|


## WifiP2pDevice<sup>8+</sup>

Represents the P2P device information.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Type| Readable/Writable| Description|
| -------- | -------- | -------- | -------- |
| deviceName | string | Read only| Device name.|
| deviceAddress | string | Read only| MAC address of the device.|
| primaryDeviceType | string | Read only| Type of the primary device.|
| deviceStatus | [P2pDeviceStatus](#p2pdevicestatus8) | Read only| Device status.|
| groupCapabilitys | number | Read only| Group capabilities.|


## P2pDeviceStatus<sup>8+</sup>

Enumerates the P2P device states.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Default Value| Description|
| -------- | -------- | -------- |
| CONNECTED | 0 | Connected.|
| INVITED | 1 | Invited.|
| FAILED | 2 | Failed.|
| AVAILABLE | 3 | Available.|
| UNAVAILABLE | 4 | Unavailable.|


## wifi.getP2pLocalDevice<sup>9+</sup>

getP2pLocalDevice(): Promise&lt;WifiP2pDevice&gt;

Obtains the local device information in a P2P connection. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[WifiP2pDevice](#wifip2pdevice8)&gt; | Promise used to return the local device information obtained.|


## wifi.getP2pLocalDevice<sup>9+</sup>

getP2pLocalDevice(callback: AsyncCallback&lt;WifiP2pDevice&gt;): void

Obtains the local device information in a P2P connection. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.GET_WIFI_CONFIG

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[WifiP2pDevice](#wifip2pdevice8)&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the local device information obtained. If **err** is not **0**, an error has occurred.|


## wifi.createGroup<sup>8+</sup>

createGroup(config: WifiP2PConfig): boolean

Creates a P2P group.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

  | **Name**| **Type**| Mandatory| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiP2PConfig](#wifip2pconfig8) | Yes| Group configuration.|

**Return value**
  | Type| Description|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## WifiP2PConfig<sup>8+</sup>

Represents P2P configuration.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Type| Readable/Writable| Description|
| -------- | -------- | -------- | -------- |
| deviceAddress | string | Read only| Device address.|
| netId | number | Read only| Network ID. The value **-1** indicates a temporary group, and **-2** indicates a persistent group.|
| passphrase | string | Read only| Passphrase of the group.|
| groupName | string | Read only| Name of the group.|
| goBand | [GroupOwnerBand](#groupownerband8) | Read only| Frequency band of the group.|


## GroupOwnerBand<sup>8+</sup>

Enumerates the P2P group frequency bands.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Default Value| Description|
| -------- | -------- | -------- |
| GO_BAND_AUTO | 0 | Auto.|
| GO_BAND_2GHZ | 1 | 2 GHz.|
| GO_BAND_5GHZ | 2 | 5 GHz.|


## wifi.removeGroup<sup>8+</sup>

removeGroup(): boolean

Removes this P2P group.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.p2pConnect<sup>8+</sup>

p2pConnect(config: WifiP2PConfig): boolean

Sets up a P2P connection.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

  | **Name**| **Type**| Mandatory| **Description**|
  | -------- | -------- | -------- | -------- |
  | config | [WifiP2PConfig](#wifip2pconfig8) | Yes| Connection configuration.|

**Return value**
  | Type| Description|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


**Example**
  ```js
  import wifi from '@ohos.wifi';
  
  var recvP2pConnectionChangeFunc = result => {
      console.info("p2p connection change receive event: " + JSON.stringify(result));
      wifi.getP2pLinkedInfo((err, data) => {
          if (err) {
              console.error('failed to get getP2pLinkedInfo: ' + JSON.stringify(err));
              return;
          }
          console.info("get getP2pLinkedInfo: " + JSON.stringify(data));
      });
  }
  wifi.on("p2pConnectionChange", recvP2pConnectionChangeFunc);
  
  var recvP2pDeviceChangeFunc = result => {
      console.info("p2p device change receive event: " + JSON.stringify(result));
  }
  wifi.on("p2pDeviceChange", recvP2pDeviceChangeFunc);
  
  var recvP2pPeerDeviceChangeFunc = result => {
      console.info("p2p peer device change receive event: " + JSON.stringify(result));
      wifi.getP2pPeerDevices((err, data) => {
          if (err) {
              console.error('failed to get peer devices: ' + JSON.stringify(err));
              return;
          }
          console.info("get peer devices: " + JSON.stringify(data));
          var len = Object.keys(data).length;
          for (var i = 0; i < len; ++i) {
              if (data[i].deviceName === "my_test_device") {
                  console.info("p2p connect to test device: " + data[i].deviceAddress);
                  var config = {
                      "deviceAddress":data[i].deviceAddress,
                      "netId":-2,
                      "passphrase":"",
                      "groupName":"",
                      "goBand":0,
                  }
                  wifi.p2pConnect(config);
              }
          }
      });
  }
  wifi.on("p2pPeerDeviceChange", recvP2pPeerDeviceChangeFunc);
  
  var recvP2pPersistentGroupChangeFunc = () => {
      console.info("p2p persistent group change receive event");
  
      wifi.getCurrentGroup((err, data) => {
          if (err) {
              console.error('failed to get current group: ' + JSON.stringify(err));
              return;
          }
          console.info("get current group: " + JSON.stringify(data));
      });
  }
  wifi.on("p2pPersistentGroupChange", recvP2pPersistentGroupChangeFunc);
  
  setTimeout(function() {wifi.off("p2pConnectionChange", recvP2pConnectionChangeFunc);}, 125 * 1000);
  setTimeout(function() {wifi.off("p2pDeviceChange", recvP2pDeviceChangeFunc);}, 125 * 1000);
  setTimeout(function() {wifi.off("p2pPeerDeviceChange", recvP2pPeerDeviceChangeFunc);}, 125 * 1000);
  setTimeout(function() {wifi.off("p2pPersistentGroupChange", recvP2pPersistentGroupChangeFunc);}, 125 * 1000);
  console.info("start discover devices -> " + wifi.startDiscoverDevices());
  ```

## wifi.p2pCancelConnect<sup>8+</sup>

p2pCancelConnect(): boolean

Cancels this P2P connection.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.startDiscoverDevices<sup>8+</sup>

startDiscoverDevices(): boolean

Starts to discover devices.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.stopDiscoverDevices<sup>8+</sup>

stopDiscoverDevices(): boolean

Stops discovering devices.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.deletePersistentGroup<sup>8+</sup>

deletePersistentGroup(netId: number): boolean

Deletes a persistent group.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**

  | **Name**| **Type**| Mandatory| **Description**|
  | -------- | -------- | -------- | -------- |
  | netId | number | Yes| ID of a group to delete.|

**Return value**
  | Type| Description|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.getP2pGroups<sup>9+</sup>
This is a system API.

getP2pGroups(): Promise&lt;Array&lt;WifiP2pGroupInfo&gt;&gt;

Obtains information about all P2P groups. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Return value**
  | Type| Description|
  | -------- | -------- |
  | Promise&lt;&nbsp;Array&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo8)&gt;&nbsp;&gt; | Promise used to return the group information obtained.|


## WifiP2pGroupInfo<sup>8+</sup>

Represents the P2P group information.

**System capability**: SystemCapability.Communication.WiFi.P2P

| Name| Type| Readable/Writable| Description|
| -------- | -------- | -------- | -------- |
| isP2pGo | boolean | Read only| Whether the device is the group owner.|
| ownerInfo | [WifiP2pDevice](#wifip2pdevice8) | Read only| Device information of the group.|
| passphrase | string | Read only| Passphrase of the group.|
| interface | string | Read only| Interface name.|
| groupName | string | Read only| Group name.|
| networkId | number | Read only| Network ID.|
| frequency | number | Read only| Frequency of the group.|
| clientDevices | [WifiP2pDevice[]](#wifip2pdevice8) | Read only| List of connected devices.|
| goIpAddress | string | Read only| IP address of the group.|


## wifi.getP2pGroups<sup>9+</sup>

getP2pGroups(callback: AsyncCallback&lt;Array&lt;WifiP2pGroupInfo&gt;&gt;): void

Obtains information about all P2P groups. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;&nbsp;Array&lt;[WifiP2pGroupInfo](#wifip2pgroupinfo8)&gt;&gt; | Yes| Callback invoked to return the result. If the operation is successful, **err** is **0** and **data** is the group information obtained. If **err** is not **0**, an error has occurred.|


## wifi.setDeviceName<sup>8+</sup>

setDeviceName(devName: string): boolean

Sets the device name.
This is a system API.

**Required permissions**:
  ohos.permission.SET_WIFI_INFO and ohos.permission.MANAGE_WIFI_CONNECTION (available only to system applications)

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | devName | string | Yes| Device name to set.|

**Return value**
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifi.on('wifiStateChange')<sup>7+</sup>

on(type: "wifiStateChange", callback: Callback&lt;number&gt;): void

Registers the WLAN state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **wifiStateChange**.|
  | callback | Callback&lt;number&gt; | Yes| Callback invoked to return the WLAN state.|

**WLAN states** 

| **Value**| **Description**|
| -------- | -------- |
| 0 | Deactivated|
| 1 | Activated|
| 2 | Activating|
| 3 | Deactivating|


## wifi.off('wifiStateChange')<sup>7+</sup>

off(type: "wifiStateChange", callback?: Callback&lt;number&gt;): void

Unregisters the WLAN state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **wifiStateChange**.|
  | callback | Callback&lt;number&gt; | No| Callback used to return the WLAN state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|

**Example**
  ```js
  import wifi from '@ohos.wifi';
  
  var WIFI_POWER_STATE = "wifiStateChange";
  var recvPowerNotifyFunc = result => {
      console.info("Receive power state change event: " + result);
  }
  
  // Register an event.
  wifi.on(WIFI_POWER_STATE, recvPowerNotifyFunc);
  
  // Unregister an event.
  wifi.off(WIFI_POWER_STATE, recvPowerNotifyFunc);
  ```


## wifi.on('wifiConnectionChange')<sup>7+</sup>

on(type: "wifiConnectionChange", callback: Callback&lt;number&gt;): void

Registers the WLAN connection state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **wifiConnectionChange**.|
  | callback | Callback&lt;number&gt; | Yes| Callback invoked to return the WLAN connection state.|

**WLAN connection states**

| **Value**| **Description**|
| -------- | -------- |
| 0 | Disconnected|
| 1 | Connected|


## wifi.off('wifiConnectionChange')<sup>7+</sup>

off(type: "wifiConnectionChange", callback?: Callback&lt;number&gt;): void

Unregisters the WLAN connection state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **wifiConnectionChange**.|
  | callback | Callback&lt;number&gt; | No| Callback used to return the WLAN connection state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


## wifi.on('wifiScanStateChange')<sup>7+</sup>

on(type: "wifiScanStateChange", callback: Callback&lt;number&gt;): void

Registers the WLAN scan state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **wifiScanStateChange**.|
  | callback | Callback&lt;number&gt; | Yes| Callback invoked to return the WLAN scan state.|

**WLAN scan states**

| **Value**| **Description**|
| -------- | -------- |
| 0 | Scan failed|
| 1 | Scan successful|


## wifi.off('wifiScanStateChange')<sup>7+</sup>

off(type: "wifiScanStateChange", callback?: Callback&lt;number&gt;): void

Unregisters the WLAN scan state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**

| **Name**| **Type**| **Mandatory**| **Description**|
| -------- | -------- | -------- | -------- |
| type | string | Yes| Event type. The value is **wifiScanStateChange**.|
| callback | Callback&lt;number&gt; | No| Callback used to return the WLAN scan state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


## wifi.on('wifiRssiChange')<sup>7+</sup>

on(type: "wifiRssiChange", callback: Callback&lt;number&gt;): void

Registers the RSSI change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **wifiRssiChange**.|
  | callback | Callback&lt;number&gt; | Yes| Callback invoked to return the RSSI, in dBm.|


## wifi.off('wifiRssiChange')<sup>7+</sup>

off(type: "wifiRssiChange", callback?: Callback&lt;number&gt;): void

Unregisters the RSSI change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.STA

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **wifiRssiChange**.|
  | callback | Callback&lt;number&gt; | No| Callback used to return the RSSI. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


## wifi.on('hotspotStateChange')<sup>7+</sup>

on(type: "hotspotStateChange", callback: Callback&lt;number&gt;): void

Registers the hotspot state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **hotspotStateChange**.|
  | callback | Callback&lt;number&gt; | Yes| Callback invoked to return the hotspot state.|

**Hotspot states**

| **Value**| **Description**|
| -------- | -------- |
| 0 | Deactivated|
| 1 | Activated|
| 2 | Activating|
| 3 | Deactivating|


## wifi.off('hotspotStateChange')<sup>7+</sup>

off(type: "hotspotStateChange", callback?: Callback&lt;number&gt;): void

Unregisters the hotspot state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.AP.Core

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **hotspotStateChange**.|
  | callback | Callback&lt;number&gt; | No| Callback used to return the hotspot state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


## wifi.on('p2pStateChange')<sup>8+</sup>

on(type: "p2pStateChange", callback: Callback&lt;number&gt;): void

Registers the P2P state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pStateChange**.|
  | callback | Callback&lt;number&gt; | Yes| Callback invoked to return the P2P state.|

**P2P states**

| **Value**| **Description**|
| -------- | -------- |
| 1 | Available|
| 2 | Opening|
| 3 | Opened|
| 4 | Closing|
| 5 | Closed|

## wifi.off('p2pStateChange')<sup>8+</sup>

off(type: "p2pStateChange", callback?: Callback&lt;number&gt;): void

Unregisters the P2P state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pStateChange**.|
  | callback | Callback&lt;number&gt; | No| Callback used to return the P2P state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


  ## wifi.on('p2pConnectionChange')<sup>8+</sup>

on(type: "p2pConnectionChange", callback: Callback&lt;WifiP2pLinkedInfo&gt;): void

Registers the P2P connection state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pConnectionChange**.|
  | callback | Callback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo8)&gt; | Yes| Callback invoked to return the P2P connection state.|


## wifi.off('p2pConnectionChange')<sup>8+</sup>

off(type: "p2pConnectionChange", callback?: Callback&lt;WifiP2pLinkedInfo&gt;): void

Unregisters the P2P connection state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pConnectionChange**.|
  | callback | Callback&lt;[WifiP2pLinkedInfo](#wifip2plinkedinfo8)&gt; | No| Callback used to return the P2P connection state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


## wifi.on('p2pDeviceChange')<sup>8+</sup>

on(type: "p2pDeviceChange", callback: Callback&lt;WifiP2pDevice&gt;): void

Registers the P2P device state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pDeviceChange**.|
  | callback | Callback&lt;[WifiP2pDevice](#wifip2pdevice8)&gt; | Yes| Callback invoked to return the P2P device state.|


## wifi.off('p2pDeviceChange')<sup>8+</sup>

off(type: "p2pDeviceChange", callback?: Callback&lt;WifiP2pDevice&gt;): void

Unregisters the P2P device state change events.

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pDeviceChange**.|
  | callback | Callback&lt;[WifiP2pDevice](#wifip2pdevice8)&gt; | No| Callback used to return the P2P device state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


## wifi.on('p2pPeerDeviceChange')<sup>8+</sup>

on(type: "p2pPeerDeviceChange", callback: Callback&lt;WifiP2pDevice[]&gt;): void

Registers the P2P peer device state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO and ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pPeerDeviceChange**.|
  | callback | Callback&lt;[WifiP2pDevice[]](#wifip2pdevice8)&gt; | Yes| Callback invoked to return the P2P peer device state.|


## wifi.off('p2pPeerDeviceChange')<sup>8+</sup>

off(type: "p2pPeerDeviceChange", callback?: Callback&lt;WifiP2pDevice[]&gt;): void

Unregisters the P2P peer device state change events.

**Required permissions**: ohos.permission.LOCATION

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pPeerDeviceChange**.|
  | callback | Callback&lt;[WifiP2pDevice[]](#wifip2pdevice8)&gt; | No| Callback used to return the peer device state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


## wifi.on('p2pPersistentGroupChange')<sup>8+</sup>

on(type: "p2pPersistentGroupChange", callback: Callback&lt;void&gt;): void

Registers the P2P persistent group state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pPersistentGroupChange**.|
  | callback | Callback&lt;void&gt; | Yes| Callback invoked to return the P2P persistent group state.|


## wifi.off('p2pPersistentGroupChange')<sup>8+</sup>

off(type: "p2pPersistentGroupChange", callback?: Callback&lt;void&gt;): void

Unregisters the P2P persistent group state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pPersistentGroupChange**.|
  | callback | Callback&lt;void&gt; | No| Callback used to return the P2P persistent group state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|


## wifi.on('p2pDiscoveryChange')<sup>8+</sup>

on(type: "p2pDiscoveryChange", callback: Callback&lt;number&gt;): void

Registers the P2P device discovery state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pDiscoveryChange**.|
  | callback | Callback&lt;number&gt; | Yes| Callback invoked to return the P2P device discovery state.|

**P2P discovered device states**

| **Value**| **Description**|
| -------- | -------- |
| 0 | Initial state|
| 1 | Discovered|


## wifi.off('p2pDiscoveryChange')<sup>8+</sup>

off(type: "p2pDiscoveryChange", callback?: Callback&lt;number&gt;): void

Unregisters the P2P device discovery state change events.

**Required permissions**: ohos.permission.GET_WIFI_INFO

**System capability**: SystemCapability.Communication.WiFi.P2P

**Parameters**
  | **Name**| **Type**| **Mandatory**| **Description**|
  | -------- | -------- | -------- | -------- |
  | type | string | Yes| Event type. The value is **p2pDiscoveryChange**.|
  | callback | Callback&lt;number&gt; | No| Callback used to return the P2P device discovery state. If this parameter is not specified, all callbacks associated with the specified event will be unregistered.|
