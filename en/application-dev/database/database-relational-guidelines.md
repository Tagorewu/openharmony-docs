# RDB Development

## When to Use

A relational database (RDB) store allows you to operate local data with or without native SQL statements based on SQLite.


## Available APIs

For details about RDB APIs, see [Relational Database](../reference/apis/js-apis-data-rdb.md).

### Creating or Deleting an RDB Store

The table below describes the APIs available for creating and deleting an RDB store.

**Table 1** APIs for creating and deleting an RDB store

| API| Description|
| -------- | -------- |
|getRdbStore(context: Context, config: StoreConfig, version: number, callback: AsyncCallback&lt;RdbStore&gt;): void| Obtains an RDB store. This API uses a callback to return the result. You can set parameters for the RDB store based on service requirements, and then call APIs to perform data operations.<br>- **context**: context of the application or function.<br>- **config**: configuration of the RDB store.<br>- **version**: RDB version.<br>- **callback**: callback invoked to return the RDB store obtained.|
|getRdbStore(context: Context, config: StoreConfig, version: number): Promise&lt;RdbStore&gt; | Obtains an RDB store. This API uses a promise to return the result. You can set parameters for the RDB store based on service requirements, and then call APIs to perform data operations.<br>- **context**: context of the application or function.<br>- **config**: configuration of the RDB store.<br>- **version**: RDB version.|
|deleteRdbStore(context: Context, name: string, callback: AsyncCallback&lt;void&gt; ): void | Deletes an RDB store. This API uses a callback to return the result. <br>- **context**: context of the application or function.<br>- **name**: RDB store to delete.<br>- **callback**: callback invoked to return the result.|
| deleteRdbStore(context: Context, name: string): Promise&lt;void&gt; | Deletes an RDB store. This API uses a promise to return the result.<br>- **context**: context of the application or function.<br>- **name**: RDB store to delete.|

### Managing Data in an RDB Store

The RDB provides APIs for inserting, deleting, updating, and querying data in the local RDB store.

- **Inserting data**
  
  The RDB provides APIs for inserting data through a **ValuesBucket** in a data table. If the data is inserted, the row ID of the data inserted will be returned; otherwise, **-1** will be returned.
  
  **Table 2** APIs for inserting data
  
  | Class| API| Description|
  | -------- | -------- | -------- |
  | RdbStore | insert(table: string, values: ValuesBucket, callback: AsyncCallback&lt;number&gt;):void | Inserts a row of data into a table. This API uses a callback to return the result.<br>- **table**: name of the target table.<br>- **values**: data to be inserted into the table.<br>- **callback**: callback invoked to return the result. If the operation is successful, the row ID will be returned; otherwise, **-1** will be returned.|
  | RdbStore | insert(table: string, values: ValuesBucket): Promise&lt;number&gt; | Inserts a row of data into a table. This API uses a promise to return the result.<br>- **table**: name of the target table.<br>- **values**: data to be inserted into the table.|
  
- **Updating data**
  
  Call the **update()** method to pass new data and specify the update conditions by using **RdbPredicates**. If the data is updated, the number of rows of the updated data will be returned; otherwise, **0** will be returned.
  
  **Table 3** APIs for updating data
  
  | Class| API| Description|
  | -------- | -------- | -------- |
  | RdbStore | update(values: ValuesBucket, predicates: RdbPredicates, callback: AsyncCallback&lt;number&gt;):void | Updates data in the RDB store based on the specified **RdbPredicates** object. This API uses a callback to return the result.<br>- **values**: data to update, which is stored in a **ValuesBucket**.<br>- **predicates**: conditions for updating data.<br>- **callback**: callback invoked to return the number of rows updated.|
  | RdbStore | update(values: ValuesBucket, predicates: RdbPredicates): Promise&lt;number&gt; | Updates data in the RDB store based on the specified **RdbPredicates** object. This API uses a promise to return the result.<br>- **values**: data to update, which is stored in a **ValuesBucket**.<br>- **predicates**: conditions for updating data.|
  
- **Deleting data**
  
  Call the **delete()** method to delete data meeting the conditions specified by **RdbPredicates**. If the data is deleted, the number of rows of the deleted data will be returned; otherwise, **0** will be returned.
  
  **Table 4** APIs for deleting data
  
  | Class| API| Description|
  | -------- | -------- | -------- |
  | RdbStore | delete(predicates: RdbPredicates, callback: AsyncCallback&lt;number&gt;):void | Deletes data from the RDB store based on the specified **RdbPredicates** object. This API uses an asynchronous callback to return the result.<br>- **predicates**: conditions for deleting data.<br>- **callback**: callback invoked to return the number of rows updated.|
  | RdbStore | delete(predicates: RdbPredicates): Promise&lt;number&gt; | Deletes data from the RDB store based on the specified **RdbPredicates** object. This API uses a promise to return the result.<br>- **predicates**: conditions for deleting data.|
  
- **Querying data**

  You can query data in an RDB store in either of the following ways:

  - Call the **query()** method to query data based on the predicates, without passing any SQL statement.
  - Run the native SQL statement.

  **Table 5** APIs for querying data

  | Class| API| Description|
  | -------- | -------- | -------- |
  | RdbStore | query(predicates: RdbPredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;ResultSet&gt;): void | Queries data in the RDB store based on the specified **RdbPredicates** object. This API uses a callback to return the result.<br>- **predicates**: conditions for querying data.<br>- **columns**: columns to query. If this parameter is not specified, the query applies to all columns.<br>- **callback**: callback invoked to return the result. If the operation is successful, a **ResultSet** object will be returned.|
  | RdbStore | query(predicates: RdbPredicates, columns?: Array&lt;string&gt;): Promise&lt;ResultSet&gt; | Queries data in the RDB store based on the specified **RdbPredicates** object. This API uses a promise to return the result.<br>- **predicates**: conditions for querying data.<br>- **columns**: columns to query. If this parameter is not specified, the query applies to all columns.|
  | RdbStore | querySql(sql: string, bindArgs: Array&lt;ValueType&gt;, callback: AsyncCallback&lt;ResultSet&gt;):void | Queries data in the RDB store using the specified SQL statement. This API uses a callback to return the result.<br>- **sql**: SQL statement.<br>- **bindArgs**: arguments in the SQL statement.<br>- **callback**: callback invoked to return the result. If the operation is successful, a **ResultSet** object will be returned.|
  | RdbStore | querySql(sql: string, bindArgs?: Array&lt;ValueType&gt;):Promise&lt;ResultSet&gt; | Queries data in the RDB store using the specified SQL statement. This API uses a promise to return the result.<br>- **sql**: SQL statement.<br>- **bindArgs**: arguments in the SQL statement.|
  | RdbStore | remoteQuery(device: string, table: string, predicates: RdbPredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;ResultSet&gt;): void |Queries data from the RDB store of a remote device based on specified conditions. This API uses an asynchronous callback to return the result.<br>- **device**: network ID of the remote device.<br>- **table**: name of the table to query.<br>- **predicates**: conditions for querying data.<br>- **columns**: columns to query. If this parameter is not specified, the query applies to all columns.<br>- **callback**: callback invoked to return the result. If the operation is successful, a **ResultSet** object will be returned.|
  | RdbStore | remoteQuery(device: string, table: string, predicates: RdbPredicates, columns: Array&lt;string&gt;): Promise&lt;ResultSet&gt; | Queries data from the RDB store of a remote device based on specified conditions. This API uses a promise to return the result.<br>- **device**: network ID of the remote device.<br>- **table**: name of the table to query.<br>- **predicates**: conditions for querying data.<br>- **columns**: columns to query. If this parameter is not specified, the query applies to all columns.|

### Using Predicates

The RDB provides **RdbPredicates** for you to set database operation conditions.

**Table 6** APIs for using RDB store predicates

| Class| API| Description|
| -------- | -------- | -------- |
| RdbPredicates |inDevices(devices: Array\<string>): RdbPredicates | Specifies remote devices on the network with RDB stores to be synchronized.<br>- **devices**: IDs of the remote devices on the network.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates |inAllDevices(): RdbPredicates | Connects to all remote devices on the network with RDB stores to be synchronized.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | equalTo(field: string, value: ValueType): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **ValueType** and value equal to the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | notEqualTo(field: string, value: ValueType): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **ValueType** and value not equal to the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | beginWrap(): RdbPredicates | Adds a left parenthesis to the **RdbPredicates**.<br>- **RdbPredicates**: returns a **RdbPredicates** with a left parenthesis.|
| RdbPredicates | endWrap(): RdbPredicates | Adds a right parenthesis to the **RdbPredicates**.<br>- **RdbPredicates**: returns a **RdbPredicates** with a right parenthesis.|
| RdbPredicates | or(): RdbPredicates | Adds the OR condition to the **RdbPredicates**.<br>- **RdbPredicates**: returns a **RdbPredicates** with the OR condition.|
| RdbPredicates | and(): RdbPredicates | Adds the AND condition to the **RdbPredicates**.<br>- **RdbPredicates**: returns a **RdbPredicates** with the AND condition.|
| RdbPredicates | contains(field: string, value: string): RdbPredicates | Sets an **RdbPredicates** to match a string containing the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified string.|
| RdbPredicates | beginsWith(field: string, value: string): RdbPredicates | Sets an **RdbPredicates** to match a string that starts with the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | endsWith(field: string, value: string): RdbPredicates | Sets an **RdbPredicates** to match a string that ends with the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | isNull(field: string): RdbPredicates | Sets an **RdbPredicates** to match the field whose value is null.<br>- **field**: column name in the database table.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | isNotNull(field: string): RdbPredicates | Sets an **RdbPredicates** to match the field whose value is not null.<br>- **field**: column name in the database table.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | like(field: string, value: string): RdbPredicates | Sets an **RdbPredicates** to match a string that is similar to the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | glob(field: string, value: string): RdbPredicates | Sets an **RdbPredicates** to match the specified string.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | between(field: string, low: ValueType, high: ValueType): RdbPredicates | Sets ta **RdbPredicates** to match the field with data type **ValueType** and value within the specified range.<br>- **field**: column name in the database table.<br>- **low**: minimum value that matches the **RdbPredicates**.<br>- **high**: maximum value that matches the **RdbPredicates**.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | notBetween(field: string, low: ValueType, high: ValueType): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **ValueType** and value out of the specified range.<br>- **field**: column name in the database table.<br>- **low**: minimum value that matches the **RdbPredicates**.<br>- **high**: maximum value that matches the **RdbPredicates**.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | greaterThan(field: string, value: ValueType): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **ValueType** and value greater than the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | lessThan(field: string, value: ValueType): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **ValueType** and value less than the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | greaterThanOrEqualTo(field: string, value: ValueType): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **ValueType** and value greater than or equal to the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | lessThanOrEqualTo(field: string, value: ValueType): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **ValueType** and value less than or equal to the specified value.<br>- **field**: column name in the database table.<br>- **value**: value specified.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | orderByAsc(field: string): RdbPredicates | Sets an **RdbPredicates** to match the column with values sorted in ascending order.<br>- **field**: column name in the database table.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | orderByDesc(field: string): RdbPredicates | Sets an **RdbPredicates** to match the column with values sorted in descending order.<br>- **field**: column name in the database table.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | distinct(): RdbPredicates | Sets an **RdbPredicates** to filter out duplicate records.<br>- **RdbPredicates**: returns a **RdbPredicates** object that can filter out duplicate records.|
| RdbPredicates | limitAs(value: number): RdbPredicates | Sets an **RdbPredicates** to specify the maximum number of records.<br>- **value**: maximum number of records.<br>- **RdbPredicates**: returns a **RdbPredicates** object that can be used to set the maximum number of records.|
| RdbPredicates | offsetAs(rowOffset: number): RdbPredicates | Sets the **RdbPredicates** to specify the start position of the returned result.<br>- **rowOffset**: start position of the returned result. The value is a positive integer.<br>- **RdbPredicates**: returns a **RdbPredicates** object that specifies the start position of the returned result.|
| RdbPredicates | groupBy(fields: Array&lt;string&gt;): RdbPredicates | Sets an **RdbPredicates** to group rows that have the same value into summary rows.<br>- **fields**: names of the columns grouped for querying data.<br>- **RdbPredicates**: returns a **RdbPredicates** object that groups rows with the same value.|
| RdbPredicates | indexedBy(indexName: string): RdbPredicates | Sets an **RdbPredicates** to specify the index column.<br>- **indexName**: name of the index column.<br>- **RdbPredicates**: returns a **RdbPredicates** object that specifies the index column.|
| RdbPredicates | in(field: string, value: Array&lt;ValueType&gt;): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **Array&#60;ValueType&#62;** and value within the specified range.<br>- **field**: column name in the database table.<br>- **value**: array of **ValueType** to match.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|
| RdbPredicates | notIn(field: string, value: Array&lt;ValueType&gt;): RdbPredicates | Sets an **RdbPredicates** to match the field with data type **Array&#60;ValueType&#62;** and value out of the specified range.<br>- **field**: column name in the database table.<br>- **value**: array of **ValueType** to match.<br>- **RdbPredicates**: returns a **RdbPredicates** object that matches the specified field.|

### Using the Result Set

A result set can be regarded as a row of data in the queried results. It allows you to traverse and access the data you have queried. The following table describes the external APIs of **ResultSet**.

> **NOTICE**<br>
> After a result set is used, you must call the **close()** method to close it explicitly.

**Table 7** APIs for using the result set

| Class| API| Description|
| -------- | -------- | -------- |
| ResultSet | goTo(offset:number): boolean | Moves the result set forwards or backwards by the specified offset relative to its current position.|
| ResultSet | goToRow(position: number): boolean | Moves the result set to the specified row.|
| ResultSet | goToNextRow(): boolean | Moves the result set to the next row.|
| ResultSet | goToPreviousRow(): boolean | Moves the result set to the previous row.|
| ResultSet | getColumnIndex(columnName: string): number | Obtains the column index based on the specified column name.|
| ResultSet | getColumnName(columnIndex: number): string | Obtains the column name based on the specified column index.|
| ResultSet | goToFirstRow(): boolean | Moves to the first row of the result set.|
| ResultSet | goToLastRow(): boolean | Moves to the last row of the result set.|
| ResultSet | getString(columnIndex: number): string | Obtains the value in the specified column of the current row, in a string.|
| ResultSet | getBlob(columnIndex: number): Uint8Array | Obtains the values in the specified column of the current row, in a byte array.|
| ResultSet | getDouble(columnIndex: number): number | Obtains the values in the specified column of the current row, in double.|
| ResultSet | isColumnNull(columnIndex: number): boolean | Checks whether the value in the specified column of the current row is null.|
| ResultSet | close(): void | Closes the result set.|



### Setting Distributed Tables

>**CAUTION**<br>ohos.permission.DISTRIBUTED_DATASYNC is required for using the **setDistributedTables**, **obtainDistributedTableName**, **sync**, **on**, and **off** APIs of **RdbStore**.

**Setting Distributed Tables**

**Table 8** APIs for setting distributed tables

| Class| API| Description|
| -------- | -------- | -------- |
| RdbStore | setDistributedTables(tables: Array\<string>, callback: AsyncCallback\<void>): void | Sets a list of distributed tables. This API uses a callback to return the result.<br>- **tables**: names of the distributed tables to set.<br>- **callback**: callback invoked to return the result.|
| RdbStore | setDistributedTables(tables: Array\<string>): Promise\<void> | Sets a list of distributed tables. This API uses a promise to return the result.<br>- **tables**: names of the distributed tables to set.|

**Obtaining the Distributed Table Name for a Remote Device**

You can obtain the distributed table name for a remote device based on the local table name. The distributed table name can be used to query the RDB store of the remote device.

**Table 9** APIs for obtaining the distributed table name of a remote device

| Class| API| Description|
| -------- | -------- | -------- |
| RdbStore | obtainDistributedTableName(device: string, table: string, callback: AsyncCallback\<string>): void | Obtains the distributed table name for a remote device based on the local table name. The distributed table name is required when the database of a remote device is queried. This API uses an asynchronous callback to return the result.<br>- **device**: remote device.<br>- **table**: local table name.<br>- **callback**: callback used to return the result. If the operation is successful, the distributed table name of the remote device will be returned.|
| RdbStore | obtainDistributedTableName(device: string, table: string): Promise\<string> | Obtains the distributed table name for a remote device based on the local table name. The distributed table name is used to query the RDB store of the remote device. This API uses a promise to return the result.<br>- **device**: remote device.<br>- **table**: local table name.|

**Synchronizing Data Between Devices**

**Table 10** APIs for synchronizing data between devices

| Class| API| Description|
| -------- | -------- | -------- |
| RdbStore | sync(mode: SyncMode, predicates: RdbPredicates, callback: AsyncCallback\<Array\<[string, number]>>): void | Synchronizes data between devices. This API uses a callback to return the result.<br>- **mode**: data synchronization mode.  **SYNC_MODE_PUSH** means to push data from the local device to a remote device. **SYNC_MODE_PULL** means to pull data from a remote device to the local device.<br>- **predicates**: data and devices to be synchronized.<br>- **callback**: callback invoked to return the result. In the result, **string** indicates the device ID, and **number** indicates the synchronization status of each device. The value **0** indicates a success, and other values indicate a failure.|
| RdbStore | sync(mode: SyncMode, predicates: RdbPredicates): Promise\<Array\<[string, number]>> | Synchronizes data between devices. This API uses a promise to return the result.<br>- **mode**: data synchronization mode.  **SYNC_MODE_PUSH** means to push data from the local device to a remote device. **SYNC_MODE_PULL** means to pull data from a remote device to the local device.<br>- **predicates**: data and devices to be synchronized.|

**Registering an RDB Store Observer**

**Table 11** API for registering an observer

| Class| API| Description|
| -------- | -------- | -------- |
| RdbStore |on(event: 'dataChange', type: SubscribeType, observer: Callback\<Array\<string>>): void| Registers an observer for this RDB store to subscribe to distributed data changes. When data in the RDB store changes, a callback will be invoked to return the data changes.<br>- **type**: subscription type. **SUBSCRIBE_TYPE_REMOTE** means to subscribe to remote data changes.<br>- **observer**: observer that listens for data changes in the RDB store.|

**Unregistering an RDB Store Observer**

**Table 12** API for unregistering an observer

| Class| API| Description|
| -------- | -------- | -------- |
| RdbStore |off(event:'dataChange', type: SubscribeType, observer: Callback\<Array\<string>>): void;| Unregisters the observer of the specified type for the RDB store. This API uses a callback to return the result.<br>- **type**: subscription type. **SUBSCRIBE_TYPE_REMOTE** means to subscribe to remote data changes.<br>- **observer**: observer to unregister.|

### Backing Up and Restoring an RDB Store

**Backing Up an RDB Store**

**Table 13** APIs for backing up an RDB store

| Class| API| Description|
| -------- | -------- | -------- |
| RdbStore |backup(destName:string, callback: AsyncCallback&lt;void&gt;):void| Backs up an RDB store. This API uses an asynchronous callback to return the result.<br>- **destName**: name of the RDB backup file.<br>- **callback**: callback invoked to return the result.|
| RdbStore |backup(destName:string): Promise&lt;void&gt;| Backs up an RDB store. This API uses a promise to return the result.<br>- **destName**: name of the RDB backup file.|

**Restoring an RDB Store**

**Table 14** APIs for restoring an RDB store

| Class| API| Description|
| -------- | -------- | -------- |
| RdbStore |restore(srcName:string, callback: AsyncCallback&lt;void&gt;):void| Restores an RDB store using a backup file. This API uses an asynchronous callback to return the result.<br>- **srcName**: name of the RDB backup file.<br>- **callback**: callback invoked to return the result.|
| RdbStore |restore(srcName:string): Promise&lt;void&gt;| Restores an RDB store using a backup file. This API uses a promise to return the result.<br>- **srcName**: name of the RDB backup file.|

**Transaction**

Table 15 Transaction APIs

| Class| API| Description|
| -------- | -------- | -------- |
| RdbStore |beginTransaction():void| Starts the transaction before executing SQL statements.|
| RdbStore |commit():void| Commits the executed SQL statements.|
| RdbStore |rollBack():void| Rolls back the SQL statements that have been executed.|

## How to Develop

1. Create an RDB store.

   (1) Configure the RDB store attributes, including the RDB store name, storage mode, and whether read-only mode is used.

   (2) Initialize the table structure and related data in the RDB store.

   (3) Create an RDB store.

   The sample code is as follows:

    ```js
    import data_rdb from '@ohos.data.rdb'

    const CREATE_TABLE_TEST = "CREATE TABLE IF NOT EXISTS test (" + "id INTEGER PRIMARY KEY AUTOINCREMENT, " + "name TEXT NOT NULL, " + "age INTEGER, " + "salary REAL, " + "blobType BLOB)";
    const STORE_CONFIG = {name: "rdbstore.db",}
    data_rdb.getRdbStore(this.context, STORE_CONFIG, 1, function (err, rdbStore) {
        rdbStore.executeSql(CREATE_TABLE_TEST)
        console.info('create table done.')
    })
    ```

2. Insert data.

   (1) Create a **ValuesBucket** to store the data you need to insert.

   (2) Call the **insert()** method to insert data into the RDB store.

   The sample code is as follows:

    ```js
    var u8 = new Uint8Array([1, 2, 3])
    const valueBucket = {"name": "Tom", "age": 18, "salary": 100.5, "blobType": u8,}
    let insertPromise = rdbStore.insert("test", valueBucket)
    ```

3. Query data.

   (1) Create an **RdbPredicates** object to specify query conditions.

   (2) Call the **query()** API to query data.

   (3) Call the **resultSet()** API to obtain the result.

   The sample code is as follows:

    ```js
    let predicates = new data_rdb.RdbPredicates("test");
    predicates.equalTo("name", "Tom")
    let promisequery = rdbStore.query(predicates)
    promisequery.then((resultSet) => {
        resultSet.goToFirstRow()
        const id = resultSet.getLong(resultSet.getColumnIndex("id"))
        const name = resultSet.getString(resultSet.getColumnIndex("name"))
        const age = resultSet.getLong(resultSet.getColumnIndex("age"))
        const salary = resultSet.getDouble(resultSet.getColumnIndex("salary"))
        const blobType = resultSet.getBlob(resultSet.getColumnIndex("blobType"))
        resultSet.close()
    })
    ```

4. Set the distributed tables to be synchronized.

    (1) Add the following permission to the permission configuration file:   

    ```json
    "requestPermissions": 
      {
        "name": "ohos.permission.DISTRIBUTED_DATASYNC"
      }
    ```

    (2) Obtain the required permissions.

    (3) Set the distributed tables.

    (4) Check whether the setting is successful.

   The sample code is as follows:

    ```js
    let context = featureAbility.getContext();
    context.requestPermissionsFromUser(['ohos.permission.DISTRIBUTED_DATASYNC'], 666, function (result) {
        console.info(`result.requestCode=${result.requestCode}`)
    })
    let promise = rdbStore.setDistributedTables(["test"])
    promise.then(() => {
        console.info("setDistributedTables success.")
    }).catch((err) => {
        console.info("setDistributedTables failed.")
    })
    ```

5. Synchronize data across devices.

    (1) Construct an **RdbPredicates** object to specify remote devices within the network to be synchronized.

    (2) Call **rdbStore.sync()** to synchronize data.

    (3) Check whether the data synchronization is successful.

    The sample code is as follows:

    ```js
    let predicate = new data_rdb.RdbPredicates('test')
    predicate.inDevices(['12345678abcde'])
    let promise = rdbStore.sync(data_rdb.SyncMode.SYNC_MODE_PUSH, predicate)
    promise.then((result) => {
        console.log('sync done.')
        for (let i = 0; i < result.length; i++) {
            console.log('device=' + result[i][0] + 'status=' + result[i][1])
        }
    }).catch((err) => {
        console.log('sync failed')
    })
    ```

6. Subscribe to distributed data.
  
    (1) Register an observer to listen for distributed data changes.

    (2) When data in the RDB store changes, a callback will be invoked to return the data changes.

    The sample code is as follows:

    ```js
    function storeObserver(devices) {
        for (let i = 0; i < devices.length; i++) {
            console.log('device=' + device[i] + 'data changed')
        }
    }
    try {
        rdbStore.on('dataChange', data_rdb.SubscribeType.SUBSCRIBE_TYPE_REMOTE, storeObserver)
    } catch (err) {
        console.log('register observer failed')
    }
    ```

7. Query data across devices.
   
    (1) Obtain the distributed table name for a remote device based on the local table name.

    (2) Call the resultSet() API to obtain the result.

    The sample code is as follows:

    ```js
    let tableName = rdbStore.obtainDistributedTableName(deviceId, "test");
    let resultSet = rdbStore.querySql("SELECT * FROM " + tableName)
    ```
    
8. Query data of a remote device.
   
   
   (1) Construct a predicate object for querying distributed tables, and specify the remote distributed table name and the remote device.
   
   (2) Call the resultSet() API to obtain the result.
   
   The sample code is as follows:
   
    ```js
    let rdbPredicate = new data_rdb.RdbPredicates('employee')
    predicates.greaterThan("id", 0) 
    let promiseQuery = rdbStore.remoteQuery('12345678abcde', 'employee', rdbPredicate)
    promiseQuery.then((resultSet) => {
        while (resultSet.goToNextRow()) {
            let idx = resultSet.getLong(0);
            let name = resultSet.getString(1);
            let age = resultSet.getLong(2);
            console.info(idx + " " + name + " " + age);
        }
        resultSet.close();
    }).catch((err) => {
        console.info("failed to remoteQuery, err: " + err)
    })
    ```
   
9. Back up and restore an RDB store.

   (1) Back up the current RDB store.

   (2) Restore the RDB store using the backup file.
   
   The sample code is as follows:

    ```js
    let promiseBackup = rdbStore.backup("dbBackup.db")
    promiseBackup.then(() => {
        console.info('Backup success.')
    }).catch((err) => {
        console.info('Backup failed, err: ' + err)
    })
    ```
    ```js
    let promiseRestore = rdbStore.restore("dbBackup.db")
    promiseRestore.then(() => {
        console.info('Restore success.')
    }).catch((err) => {
        console.info('Restore failed, err: ' + err)
    })
    ```
