# Distributed Data Object Development

## When to Use

Distributed data objects allow data traversing across devices to be processed like local variables by shielding complex data interaction between devices. For the devices that form a Super Device, when data in the distributed data object of an application is added, deleted, or modified on a device, the data for the same application is also updated on the other devices. The devices can listen for data changes and online and offline status changes of other devices. 

The distributed data objects support basic data types, such as number, string, and Boolean, as well as complex data types, such as array and nested basic types.


## Available APIs

For details about the APIs related to the distributed data object, see [Distributed Data Object](../reference/apis/js-apis-data-distributedobject.md).

### Creating a Distributed Data Object Instance

Call **createDistributedObject()** to create a distributed data object instance. You can specify the attributes of the instance in **source**.


**Table 1** API for creating a distributed data object instance
| Package | API | Description |
| -------- | -------- | -------- |
| ohos.data.distributedDataObject| createDistributedObject(source: object): DistributedObject | Creates a distributed data object instance for data operations.<br>- **source**: attributes of the **distributedObject** set.<br>- **DistributedObject**: returns the distributed object created.|

### Generating a Session ID

Call **genSessionId()** to generate a session ID randomly. The generated session ID can be used to set the session ID of a distributed data object.

**Table 2** API for generating a session ID randomly
| Package | API | Description |
| -------- | -------- | -------- |
| ohos.data.distributedDataObject| genSessionId(): string | Generates a session ID, which can be used as the session ID of a distributed data object.|

### Setting a SessionID for Distributed Data Objects

Call **setSessionId()** to set a session ID for a distributed data object. The session ID is a unique identifier for one collaboration across devices. The distributed data objects to be synchronized must be associated with the same session ID.

**Table 3** API for setting a session ID
| Class| API| Description|
| -------- | -------- | -------- |
| DistributedDataObject | setSessionId(sessionId?: string): boolean | Sets a session ID for distributed data objects.<br>**sessionId**: session ID of a distributed object in a trusted network. To remove a distributed data object from the network, set this parameter to "" or leave it empty.|

### Observing Data Changes

Call **on()** to subscribe to data changes of a distributed data object. In the case of data change, a callback will be invoked to return the data changes. You can use **off()** to unsubscribe from the data changes.

**Table 4** APIs for observing data changes of a distributed data object
| Class | API | Description |
| -------- | -------- | -------- |
| DistributedDataObject| on(type: 'change', callback: Callback<{ sessionId: string, fields: Array&lt;string&gt; }>): void | Subscribes to data changes.|
| DistributedDataObject| off(type: 'change', callback?: Callback<{ sessionId: string, fields: Array&lt;string&gt; }>): void | Unsubscribes from data changes.<br>**Callback**: specifies callback used to return changes of the distributed data object. If this parameter is not specified, all callbacks related to data changes will be unregistered.|

### Observing Online or Offline Status

Call **on()** to subscribe to status changes of a distributed data object. The status can be online or offline. When the status changes, a callback will be invoked to return the status. You can use **off()** to unsubscribe from the status changes.

**Table 5** APIs for observing status changes of a distributed data object
| Class | API | Description |
| -------- | -------- | -------- |
| DistributedDataObject| on(type: 'status', callback: Callback<{ sessionId: string, networkId: string, status: 'online' \| 'offline' }>): void | Subscribes to the status changes of a distributed data object.|
| DistributedDataObject| off(type: 'status', callback?: Callback<{ sessionId: string, deviceId: string, status: 'online' \| 'offline' }>): void | Unsubscribes from status changes of a distributed data object.|

### Saving a Distributed Data Object and Revoking the Data Saving Operation

Call **save()** to save a distributed data object. When the application is active, the saved data will not be released. When the application exits and restarts, the data saved on the device will be restored.

Call **revokeSave()** to revoke a distributed data object that is no longer required. If the distributed data object is saved on the local device, **revokeSave()** will delete the data from all trusted devices. If the distributed data object is not saved on the local device, **revokeSave()** will delete the data from the local device.

The saved data will be released in the following cases:

- The data is stored for more than 24 hours.
- The application has been uninstalled.
- Data is successfully restored.

**Table 6** APIs for saving a distributed data object and revoking the saving
| Class | API | Description |
| -------- | -------- | -------- |
| DistributedDataObject | save(deviceId: string): Promise&lt;SaveSuccessResponse&gt; | Saves a distributed data object. This API uses a promise to return the result. |
| DistributedDataObject | save(deviceId: string, callback: AsyncCallback&lt;SaveSuccessResponse&gt;): void | Saves a distributed data object. This API uses an asynchronous callback to return the result. |
| DistributedDataObject | revokeSave(callback: AsyncCallback&lt;RevokeSaveSuccessResponse&gt;): void | Revokes the data saving operation. This API uses an asynchronous callback to return the result. |
| DistributedDataObject | revokeSave(): Promise&lt;RevokeSaveSuccessResponse&gt; | Revokes the data saving operation. This API uses a promise to return the result. |

## How to Develop

The following example shows how to implement distributed data object synchronization.

1. Import the @ohos.data.distributedDataObject module to the development environment.

   ```js   
   import distributedObject from '@ohos.data.distributedDataObject';   
   ```
   
2. Request the permission. 
   
    Add the required permission in the **config.json** file. The sample code is as follows:
    
    ```
     {
       "module": {
           "reqPermissions": [
               {
                  "name": "ohos.permission.DISTRIBUTED_DATASYNC"
               }
           ]
       }
     }
    ```
	This permission must also be authorized by the user through a dialog box when the application is started for the first time. The sample code is as follows:
    
    ```
    import featureAbility from '@ohos.ability.featureAbility';
    
    function grantPermission() {
        console.info('grantPermission');
        let context = featureAbility.getContext();
        context.requestPermissionsFromUser(['ohos.permission.DISTRIBUTED_DATASYNC'], 666, function (result) {
            console.info(`result.requestCode=${result.requestCode}`)
    
        })
    console.info('end grantPermission');
    }
    grantPermission();
    ```
    
    
    
3. Obtain a distributed data object instance.

   The sample code is as follows:

   ```js
   var local_object = distributedObject.createDistributedObject({name:undefined, age:undefined, isVis:true, 
                  parent:undefined, list:undefined});
   var sessionId = distributedObject.genSessionId();
   ```


4. Add the synchronization network. The data objects in the synchronization network include the local and remote objects.
   
   The sample code is as follows:

   ```js
   // Local object
   var local_object = distributedObject.createDistributedObject({name:"jack", age:18, isVis:true, 
       parent:{mother:"jack mom", father:"jack Dad"}, list:[{mother:"jack mom"}, {father:"jack Dad"}]});
   local_object.setSessionId(sessionId);
   
   // Remote object
   var remote_object = distributedObject.createDistributedObject({name:undefined, age:undefined, isVis:true, 
                  parent:undefined, list:undefined});
   remote_object.setSessionId(sessionId);
   // After learning that the device goes online, the remote object synchronizes data. That is, name changes to jack and age to 18.
   ```
   
5. Observe the data changes of the distributed data object. 

   You can subscribe to data changes of the peer object. When the data in the peer object changes, a callback will be called to return the data changes.
   
   The sample code is as follows:
   
   ```js
   function changeCallback(sessionId, changeData) {
        console.info("change" + sessionId);
   
        if (changeData != null && changeData != undefined) {
            changeData.forEach(element => {
                console.info("changed !" + element + " " + local_object[element]);
        });
     }
    } 
   
    // To refresh the page in changeCallback, correctly bind (this) to the changeCallback.
    local_object.on("change", this.changeCallback.bind(this));
   ```
   
6. Modify object attributes. 

   The object attributes support basic data types (such as number, Boolean, and string) and complex data types (array and nested basic types).

   The sample code is as follows:
   ```js
   local_object.name = "jack";
   local_object.age = 19;
   local_object.isVis = false;
   local_object.parent = {mother:"jack mom", father:"jack Dad"};
   local_object.list = [{mother:"jack mom"}, {father:"jack Dad"}];
   ```

   > ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
   > 
   > For the distributed data object of the complex type, only the root attribute can be modified. The subordinate attributes cannot be modified. 

   Example:

   ```js
   // Supported modification.
   local_object.parent = {mother:"mom", father:"dad"};
   // Modification not supported.
   local_object.parent.mother = "mom";
   ```

7. Access the distributed data object. 

   Obtain the distributed data object attribute, which is the latest data on the network.

   The sample code is as follows:
   ```js
   console.info("name " + local_object["name"]); 
   ```

8. Unsubscribe from data changes. 

   You can specify the callback to unregister. If you do not specify the callback, all data change callbacks of the distributed data object will be unregistered.

   The sample code is as follows:

   ```js
   // Unregister the specified data change callback.
   local_object.off("change", changeCallback);
   // Unregister all data change callbacks. 
   local_object.off("change"); 
   ```

9. Subscribe to the status (online/offline) changes of the distributed data object. A callback will be invoked to report the status change when the target distributed data object goes online or offline.

   The sample code is as follows:

   ```js
    function statusCallback(sessionId, networkId, status) {
      this.response += "status changed " + sessionId + " " + status + " " + networkId;
    }
   
    local_object.on("status", this.statusCallback);
   ```

10. Save a distributed data object and revoke the data saving operation.

    - Callback

      ```
      ​```js
       // Save a distributed data object.
       local_object.save("local", (result, data) => {
           console.log("save callback");
           console.info("save sessionId " + data.sessionId);
           console.info("save version " + data.version);
           console.info("save deviceId " + data.deviceId);
       });
       // Revoke the data saving operation.
       local_object.revokeSave((result, data) => {
       console.log("revokeSave callback");
       console.info("revokeSave sessionId " + data.sessionId);
       });
      ​```
      ```

    - Promise

      ```
      ​```js
       // Save a distributed data object.
       g_object.save("local").then((result) => {
           console.info("save sessionId " + result.sessionId);
           console.info("save version " + result.version);
           console.info("save deviceId " + result.deviceId);
       }, (result)=>{
           console.info("save local failed.");
       });
       // Revoke the data saving operation.
       g_object.revokeSave().then((result) => {
           console.info("revokeSave success.");
       }, (result)=>{
           console.info("revokeSave failed.");
       });
      ​```
      ```

      

11. Unsubscribe from the status changes of the distributed data object. 

    You can specify the callback to unregister. If you do not specify the callback, this API unregisters all callbacks of this distributed data object.

    The sample code is as follows:
    ```js
    // Unregister the specified status change callback.
    local_object.off("status", this.statusCallback);
    // Unregister all status change callbacks.
    local_object.off("status");
    ```

12. Remove a distributed data object from the synchronization network. Data changes on the local object will not be synchronized to the removed distributed data object.

     The sample code is as follows:
       ```js
       local_object.setSessionId("");
       ```
