# Distributed Data Service Development

## When to Use

The Distributed Data Service (DDS) implements synchronization of application data across user devices. When data is added, deleted, or modified for an application on a device, the same application on another device can obtain the updated data. The DDS applies to the distributed gallery, messages, contacts, and file manager.


## Available APIs
For details about the APIs related to distributed data, see [Distributed Data Management](../reference/apis/js-apis-distributed-data.md).


**Table 1** APIs provided by the DDS

| API                                                    | Description                                           |
| ------------------------------------------------------------ | ----------------------------------------------- |
| createKVManager(config:KVManagerConfig,callback:AsyncCallback&lt;KVManager&gt;):void<br>createKVManager(config:KVManagerConfig):Promise&lt;KVManager> | Creates a **KVManager** object for database management.|
| getKVStore&lt;TextendsKVStore&gt;(storeId:string,options:Options,callback:AsyncCallback&lt;T&gt;):void<br>getKVStore&lt;TextendsKVStore&gt;(storeId:string,options:Options):Promise&lt;T&gt; | Obtains a KV store with the specified **Options** and **storeId**.|
| put(key:string,value:Uint8Array\|string\|number\|boolean,callback:AsyncCallback&lt;void&gt;):void<br>put(key:string,value:Uint8Array\|string\|number\|boolean):Promise&lt;void> | Inserts and updates data.                               |
| delete(key:string,callback:AsyncCallback&lt;void&gt;):void<br>delete(key:string):Promise&lt;void> | Deletes data.                                     |
| get(key:string,callback:AsyncCallback&lt;Uint8Array\|string\|boolean\|number&gt;):void<br>get(key:string):Promise&lt;Uint8Array\|string\|boolean\|number> | Queries data.                                     |
| on(event:'dataChange',type:SubscribeType,observer:Callback&lt;ChangeNotification&gt;):void<br>on(event:'syncComplete',syncCallback:Callback&lt;Array&lt;[string,number]&gt;&gt;):void | Subscribes to data changes in the KV store.                       |
| sync(deviceIdList:string[],mode:SyncMode,allowedDelayMs?:number):void | Triggers database synchronization in manual mode.                 |




## How to Develop

The following uses a single KV store as an example to describe the development procedure.

1. Import the distributed data module.
   ```js
   import distributedData from '@ohos.data.distributedData';
   ```

2. Create a **KvManager** instance based on the specified **KvManagerConfig** object.
   (1) Create a **KvManagerConfig** object based on the application context.
   (2) Create a **KvManager** instance.

   The sample code is as follows:
   ```js
   let kvManager;
   try {
       const kvManagerConfig = {
           bundleName : 'com.example.datamanagertest',
           userInfo : {
               userId : '0',
               userType : distributedData.UserType.SAME_USER_ID
           }
       }
       distributedData.createKVManager(kvManagerConfig, function (err, manager) {
           if (err) {
               console.log("createKVManager err: "  + JSON.stringify(err));
               return;
           }
           console.log("createKVManager success");
           kvManager = manager;
       });
   } catch (e) {
       console.log("An unexpected error occurred. Error:" + e);
   }
   ```

3. Create and obtain a single KV store.
   (1) Declare the ID of the single KV store to create.
   (2) Create a single KV store. You are advised to disable automatic synchronization (**autoSync:false**) and call **sync** when a synchronization is required.

   The sample code is as follows:
   ```js
   let kvStore;
   try {
       const options = {
           createIfMissing : true,
           encrypt : false,
           backup : false,
           autoSync : false,
           kvStoreType : distributedData.KVStoreType.SINGLE_VERSION,
           securityLevel : distributedData.SecurityLevel.S0,
       };
       kvManager.getKVStore('storeId', options, function (err, store) {
           if (err) {
               console.log("getKVStore err: "  + JSON.stringify(err));
               return;
           }
           console.log("getKVStore success");
           kvStore = store;
       });
   } catch (e) {
       console.log("An unexpected error occurred. Error:" + e);
   }
   ```

   > **NOTE**
   >
   > For data synchronization between networked devices, you are advised to open the distributed KV store during application startup to obtain the database handle. With this database handle (`kvStore` in this example), you can perform operations, such as inserting data into the KV store, without creating the KV store repeatedly during the lifecycle of the handle.
   
4. Subscribe to changes in the distributed data.<br/>
   The following is the sample code for subscribing to the data changes of a single KV store:
   ```js
   kvStore.on('dataChange', distributedData.SubscribeType.SUBSCRIBE_TYPE_ALL, function (data) {
       console.log("dataChange callback call data: " + JSON.stringify(data));
   });
   ```

5. Write data to the single KV store.
   (1) Construct the key and value to be written into the single KV store.
   (2) Write key-value pairs into the single KV store.

   The following is the sample code for writing key-value pairs of the string type into the single KV store:

   ```js
   const KEY_TEST_STRING_ELEMENT = 'key_test_string';
   const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
   try {
       kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT, function (err,data) {
           if (err != undefined) {
               console.log("put err: " + JSON.stringify(err));
               return;
           }
           console.log("put success");
       });
   }catch (e) {
       console.log("An unexpected error occurred. Error:" + e);
   }
   ```

6. Query data in the single KV store.
   (1) Construct the key to be queried from the single KV store.
   (2) Query data from the single KV store.

   The following is the sample code for querying data of the string type from the single KV store:
   ```js
   const KEY_TEST_STRING_ELEMENT = 'key_test_string';
   const VALUE_TEST_STRING_ELEMENT = 'value-test-string';
   try {
       kvStore.put(KEY_TEST_STRING_ELEMENT, VALUE_TEST_STRING_ELEMENT, function (err,data) {
           if (err != undefined) {
               console.log("put err: " + JSON.stringify(err));
               return;
           }
           console.log("put success");
           kvStore.get(KEY_TEST_STRING_ELEMENT, function (err,data) {
               console.log("get success data: " + data);
           });
       });
   }catch (e) {
       console.log("An unexpected error occurred. Error:" + e);
   }
   ```

7. Synchronize data to other devices.<br/>
   Select the devices in the same network and the synchronization mode to synchronize data.

   > **NOTE**
   >
   > The APIs of the `deviceManager` module are system interfaces.
   
   The following is a code example for synchronizing data in a single KV store:
   ```js
   import deviceManager from '@ohos.distributedHardware.deviceManager';
   
   let devManager;
   // Create deviceManager.
   deviceManager.createDeviceManager("bundleName", (err, value) => {
       if (!err) {
           devManager = value;
           // deviceIds is obtained by deviceManager by calling getTrustedDeviceListSync().
           let deviceIds = [];
           if (devManager != null) {
               var devices = devManager.getTrustedDeviceListSync();
               for (var i = 0; i < devices.length; i++) {
                   deviceIds[i] = devices[i].deviceId;
               }
           }
           try{
               // 1000 indicates that the maximum delay is 1000 ms.
               kvStore.sync(deviceIds, distributedData.SyncMode.PUSH_ONLY, 1000);
           }catch (e) {
                console.log("An unexpected error occurred. Error:" + e);
           }
       }
   });
   ```
