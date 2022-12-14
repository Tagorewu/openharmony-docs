# Result Set

A result set is a set of results returned after the relational database (RDB) query APIs are called. You can use the **resultset** APIs to obtain required data.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## ResultSetV9<sup>9+</sup>

Provides methods to access the result set, which is obtained by querying the RDB store.

### Usage

You need to obtain the **resultSetV9** instance by using [RdbStoreV9.query()](js-apis-data-rdb.md#query).

```js
import dataRdb from '@ohos.data.rdb';
let predicatesV9 = new dataRdb.RdbPredicatesV9("EMPLOYEE");
predicatesV9.equalTo("AGE", 18);
let promise = rdbStoreV9.query(predicatesV9, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSetV9) => {
    console.log(TAG + "resultSet columnNames:" + resultSetV9.columnNames);
    console.log(TAG + "resultSet columnCount:" + resultSetV9.columnCount);
});
```

### Attributes<sup>9+</sup>

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

| Name        | Type           | Mandatory| Description                            |
| ------------ | ------------------- | ---- | -------------------------------- |
| columnNames  | Array&lt;string&gt; | Yes  | Names of all columns in the result set.      |
| columnCount  | number              | Yes  | Number of columns in the result set.            |
| rowCount     | number              | Yes  | Number of rows in the result set.            |
| rowIndex     | number              | Yes  | Index of the current row in the result set.        |
| isAtFirstRow | boolean             | Yes  | Whether the cursor is in the first row of the result set.      |
| isAtLastRow  | boolean             | Yes  | Whether the cursor is in the last row of the result set.    |
| isEnded      | boolean             | Yes  | Whether the cursor is after the last row of the result set.|
| isStarted    | boolean             | Yes  | Whether the cursor has been moved.            |
| isClosed     | boolean             | Yes  | Whether the result set is closed.        |

### getColumnIndex<sup>9+</sup>

getColumnIndex(columnName: string): number

Obtains the column index based on the column name.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name    | Type  | Mandatory| Description                      |
| ---------- | ------ | ---- | -------------------------- |
| columnName | string | Yes  | Column name specified.|

**Return value**

| Type  | Description              |
| ------ | ------------------ |
| number | Index of the column obtained.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is  null or the column type is incompatible. |

**Example**

  ```js
resultSetV9.goToFirstRow();
const id = resultSetV9.getLong(resultSetV9.getColumnIndex("ID"));
const name = resultSetV9.getString(resultSetV9.getColumnIndex("NAME"));
const age = resultSetV9.getLong(resultSetV9.getColumnIndex("AGE"));
const salary = resultSetV9.getDouble(resultSetV9.getColumnIndex("SALARY"));
  ```

### getColumnName<sup>9+</sup>

getColumnName(columnIndex: number): string

Obtains the column name based on the column index.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name     | Type  | Mandatory| Description                      |
| ----------- | ------ | ---- | -------------------------- |
| columnIndex | number | Yes  | Column index specified.|

**Return value**

| Type  | Description              |
| ------ | ------------------ |
| string | Column name obtained.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is  null or the column type is incompatible. |

**Example**

  ```js
const id = resultSetV9.getColumnName(0);
const name = resultSetV9.getColumnName(1);
const age = resultSetV9.getColumnName(2);
  ```

### goTo<sup>9+</sup>

goTo(offset:number): boolean

Moves the cursor to the row based on the specified offset.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type  | Mandatory| Description                        |
| ------ | ------ | ---- | ---------------------------- |
| offset | number | Yes  | Offset relative to the current position.|

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is  empty or the specified location is invalid. |

**Example**

  ```js
let predicatesV9goto = new dataRdb.RdbPredicatesV9("EMPLOYEE");
let promisequerygoto = rdbStoreV9.query(predicatesV9goto, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promisequerygoto.then((resultSetV9) => {
    resultSetV9.goTo(1);
    resultSetV9.close();
}).catch((err) => {
    console.log('query failed');
});
  ```

### goToRow<sup>9+</sup>

goToRow(position: number): boolean

Moves the cursor to the specified row in the result set.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name  | Type  | Mandatory| Description                    |
| -------- | ------ | ---- | ------------------------ |
| position | number | Yes  | Position to which the cursor is to be moved.|

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is  empty or the specified location is invalid. |

**Example**

  ```js
let predicatesV9gotorow = new dataRdb.RdbPredicatesV9("EMPLOYEE");
let promisequerygotorow = rdbStoreV9.query(predicatesV9gotorow, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promisequerygotorow.then((resultSetV9) => {
    resultSetV9.goToRow(5);
    resultSetV9.close();
}).catch((err) => {
    console.log('query failed');
});
  ```

### goToFirstRow<sup>9+</sup>

goToFirstRow(): boolean


Moves the cursor to the first row of the result set.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is  empty or the specified location is invalid. |

**Example**

  ```js
let predicatesV9goFirst = new dataRdb.RdbPredicatesV9("EMPLOYEE");
let promisequerygoFirst = rdbStoreV9.query(predicatesV9goFirst, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promisequerygoFirst.then((resultSetV9) => {
    resultSetV9.goToFirstRow();
    resultSetV9.close();
}).catch((err) => {
    console.log('query failed');
});
  ```

### goToLastRow<sup>9+</sup>

goToLastRow(): boolean

Moves the cursor to the last row of the result set.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is  empty or the specified location is invalid. |

**Example**

  ```js
let predicatesV9goLast = new dataRdb.RdbPredicatesV9("EMPLOYEE");
let promisequerygoLast = rdbStoreV9.query(predicatesV9goLast, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promisequerygoLast.then((resultSetV9) => {
    resultSetV9.goToLastRow();
    resultSetV9.close();
}).catch((err) => {
    console.log('query failed');
});
  ```

### goToNextRow<sup>9+</sup>

goToNextRow(): boolean

Moves the cursor to the next row in the result set.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is  empty or the specified location is invalid. |

**Example**

  ```js
let predicatesV9goNext = new dataRdb.RdbPredicatesV9("EMPLOYEE");
let promisequerygoNext = rdbStoreV9.query(predicatesV9goNext, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promisequerygoNext.then((resultSetV9) => {
    resultSetV9.goToNextRow();
    resultSetV9.close();
}).catch((err) => {
    console.log('query failed');
});
  ```

### goToPreviousRow<sup>9+</sup>

goToPreviousRow(): boolean

Moves the cursor to the previous row in the result set.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is  empty or the specified location is invalid. |

**Example**

  ```js
let predicatesV9goPrev = new dataRdb.RdbPredicatesV9("EMPLOYEE");
let promisequerygoPrev = rdbStoreV9.query(predicatesV9goPrev, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promisequerygoPrev.then((resultSetV9) => {
    resultSetV9.goToPreviousRow();
    resultSetV9.close();
}).catch((err) => {
    console.log('query failed');
});
  ```

### getBlob<sup>9+</sup>

getBlob(columnIndex: number): Uint8Array

Obtains the value in the specified column in the current row as a byte array.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name     | Type  | Mandatory| Description                   |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | Yes  | Index of the specified column, starting from 0.|

**Return value**

| Type      | Description                            |
| ---------- | -------------------------------- |
| Uint8Array | Value in the specified column as a byte array.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is  null or the column type is incompatible. |

**Example**

  ```js
const codes = resultSetV9.getBlob(resultSetV9.getColumnIndex("CODES"));
  ```

### getString<sup>9+</sup>

getString(columnIndex: number): string

Obtains the value in the specified column in the current row as a string.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name     | Type  | Mandatory| Description                   |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | Yes  | Index of the specified column, starting from 0.|

**Return value**

| Type  | Description                        |
| ------ | ---------------------------- |
| string | Value in the specified column as a string.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is  null or the column type is incompatible. |

**Example**

  ```js
const name = resultSetV9.getString(resultSetV9.getColumnIndex("NAME"));
  ```

### getLong<sup>9+</sup>

getLong(columnIndex: number): number

Obtains the value in the specified column in the current row as a Long.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name     | Type  | Mandatory| Description                   |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | Yes  | Index of the specified column, starting from 0.|

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| number | Value in the specified column as a Long.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is  null or the column type is incompatible. |

**Example**

  ```js
const age = resultSetV9.getLong(resultSetV9.getColumnIndex("AGE"));
  ```

### getDouble<sup>9+</sup>

getDouble(columnIndex: number): number

Obtains the value in the specified column in the current row as a double.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name     | Type  | Mandatory| Description                   |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | Yes  | Index of the specified column, starting from 0.|

**Return value**

| Type  | Description                        |
| ------ | ---------------------------- |
| number | Value in the specified column as a double.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is  null or the column type is incompatible. |

**Example**

  ```js
const salary = resultSetV9.getDouble(resultSetV9.getColumnIndex("SALARY"));
  ```

### isColumnNull<sup>9+</sup>

isColumnNull(columnIndex: number): boolean

Checks whether the value in the specified column of the current row is null.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name     | Type  | Mandatory| Description                   |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | Yes  | Index of the specified column, starting from 0.|

**Return value**

| Type   | Description                                                     |
| ------- | --------------------------------------------------------- |
| boolean | Returns **true** if the value is null; returns **false** otherwise.|

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is  null or the column type is incompatible. |

**Example**

  ```js
const isColumnNull = resultSetV9.isColumnNull(resultSetV9.getColumnIndex("CODES"));
  ```

### close<sup>9+</sup>

close(): void

Closes this result set.

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Example**

  ```js
let predicatesV9Close = new dataRdb.RdbPredicatesV9("EMPLOYEE");
let promiseClose = rdbStoreV9.query(predicatesV9Close, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promiseClose.then((resultSetV9) => {
    resultSetV9.close();
}).catch((err) => {
    console.log('Failed to close the resultset');
});
  ```

**Error codes**

For details about the error codes, see [RDB Error Codes](../errorcodes/errorcode-data-rdb.md).

| ID| **Error Message**                                                |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is  empty or the specified location is invalid. |

## ResultSet<sup>(deprecated)</sup>

Provides methods to access the result set, which is obtained by querying the RDB store.

> **NOTE**
>
> This object is supported since API version 7 and deprecated since API version 9. You are advised to use [ResultSetV9](#resultsetv99).

### Usage

You need to obtain a **resultSet** object by using [RdbStore.query()](js-apis-data-rdb.md#query).

```js
import dataRdb from '@ohos.data.rdb';
let predicates = new dataRdb.RdbPredicates("EMPLOYEE");
predicates.equalTo("AGE", 18);
let promise = rdbStore.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
    console.log(TAG + "resultSet columnNames:" + resultSet.columnNames);
    console.log(TAG + "resultSet columnCount:" + resultSet.columnCount);
});
```

### Attributes<sup>(deprecated)</sup>

> **NOTE**
>
> This parameter is supported since API version 7 and is deprecated since API version 9. You are advised to use [Attributes](#attributes9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| columnNames | Array&lt;string&gt; | Yes| Names of all columns in the result set.|
| columnCount | number | Yes| Number of columns in the result set.|
| rowCount | number | Yes| Number of rows in the result set.|
| rowIndex | number | Yes| Index of the current row in the result set.|
| isAtFirstRow | boolean | Yes| Whether the cursor is in the first row of the result set.|
| isAtLastRow | boolean | Yes| Whether the cursor is in the last row of the result set.|
| isEnded | boolean | Yes| Whether the cursor is after the last row of the result set.|
| isStarted | boolean | Yes| Whether the cursor has been moved.|
| isClosed | boolean | Yes| Whether the result set is closed.|

### getColumnIndex<sup>(deprecated)</sup>

getColumnIndex(columnName: string): number

Obtains the column index based on the column name.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [getColumnIndex](#getcolumnindex9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| columnName | string | Yes| Column name specified.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | Index of the column obtained.|

**Example**

  ```js
  resultSet.goToFirstRow();
  const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
  const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
  const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
  const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
  ```

### getColumnName<sup>(deprecated)</sup>

getColumnName(columnIndex: number): string

Obtains the column name based on the column index.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [getColumnName](#getcolumnname9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| columnIndex | number | Yes| Column index specified.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | Column name obtained.|

**Example**

  ```js
  const id = resultSet.getColumnName(0);
  const name = resultSet.getColumnName(1);
  const age = resultSet.getColumnName(2);
  ```

### goTo<sup>(deprecated)</sup>

goTo(offset:number): boolean

Moves the cursor to the row based on the specified offset.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [goTo](#goto9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| offset | number | Yes| Offset relative to the current position.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

  ```js
  let predicatesgoto = new dataRdb.RdbPredicates("EMPLOYEE");
  let promisequerygoto = rdbStore.query(predicatesgoto, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
  promisequerygoto.then((resultSet) => {
      resultSet.goTo(1);
      resultSet.close();
  }).catch((err) => {
      console.log('query failed');
  });
  ```

### goToRow<sup>(deprecated)</sup>

goToRow(position: number): boolean

Moves the cursor to the specified row in the result set.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [goToRow](#gotorow9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| position | number | Yes| Position to which the cursor is to be moved.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

  ```js
  let predicatesgotorow = new dataRdb.RdbPredicates("EMPLOYEE");
  let promisequerygotorow = rdbStore.query(predicatesgotorow, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
  promisequerygotorow.then((resultSet) => {
      resultSet.goToRow(5);
      resultSet.close();
  }).catch((err) => {
      console.log('query failed');
  });
  ```

### goToFirstRow<sup>(deprecated)</sup>

goToFirstRow(): boolean

Moves the cursor to the first row of the result set.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [goToFirstRow](#gotofirstrow9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

  ```js
  let predicatesgoFirst = new dataRdb.RdbPredicates("EMPLOYEE");
  let promisequerygoFirst = rdbStore.query(predicatesgoFirst, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
  promisequerygoFirst.then((resultSet) => {
      resultSet.goToFirstRow();
      resultSet.close();
  }).catch((err) => {
      console.log('query failed');
  });
  ```

### goToLastRow<sup>(deprecated)</sup>

goToLastRow(): boolean

Moves the cursor to the last row of the result set.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [goToLastRow](#gotolastrow9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

  ```js
  let predicatesgoLast = new dataRdb.RdbPredicates("EMPLOYEE");
  let promisequerygoLast = rdbStore.query(predicatesgoLast, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
  promisequerygoLast.then((resultSet) => {
      resultSet.goToLastRow();
      resultSet.close();
  }).catch((err) => {
      console.log('query failed');
  });
  ```

### goToNextRow<sup>(deprecated)</sup>

goToNextRow(): boolean

Moves the cursor to the next row in the result set.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [goToNextRow](#gotonextrow9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

  ```js
  let predicatesgoNext = new dataRdb.RdbPredicates("EMPLOYEE");
  let promisequerygoNext = rdbStore.query(predicatesgoNext, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
  promisequerygoNext.then((resultSet) => {
      resultSet.goToNextRow();
      resultSet.close();
  }).catch((err) => {
      console.log('query failed');
  });
  ```

### goToPreviousRow<sup>(deprecated)</sup>

goToPreviousRow(): boolean

Moves the cursor to the previous row in the result set.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [goToPreviousRow](#gotopreviousrow9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

  ```js
  let predicatesgoPrev = new dataRdb.RdbPredicates("EMPLOYEE");
  let promisequerygoPrev = rdbStore.query(predicatesgoPrev, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
  promisequerygoPrev.then((resultSet) => {
      resultSet.goToPreviousRow();
      resultSet.close();
  }).catch((err) => {
      console.log('query failed');
  });
  ```

### getBlob<sup>(deprecated)</sup>

getBlob(columnIndex: number): Uint8Array

Obtains the value in the specified column in the current row as a byte array.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [getBlob](#getblob9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| columnIndex | number | Yes| Index of the specified column, starting from 0.|

**Return value**

| Type| Description|
| -------- | -------- |
| Uint8Array | Value in the specified column as a byte array.|

**Example**

  ```js
  const codes = resultSet.getBlob(resultSet.getColumnIndex("CODES"));
  ```

### getString<sup>(deprecated)</sup>

getString(columnIndex: number): string

Obtains the value in the specified column in the current row as a string.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [getString](#getstring9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| columnIndex | number | Yes| Index of the specified column, starting from 0.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | Value in the specified column as a string.|

**Example**

  ```js
  const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
  ```

### getLong<sup>(deprecated)</sup>

getLong(columnIndex: number): number

Obtains the value in the specified column in the current row as a Long.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [getLong](#getlong9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| columnIndex | number | Yes| Index of the specified column, starting from 0.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | Value in the specified column as a Long.|

**Example**

  ```js
  const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
  ```

### getDouble<sup>(deprecated)</sup>

getDouble(columnIndex: number): number

Obtains the value in the specified column in the current row as a double.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [getDouble](#getdouble9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| columnIndex | number | Yes| Index of the specified column, starting from 0.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | Value in the specified column as a double.|

**Example**

  ```js
  const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
  ```

### isColumnNull<sup>(deprecated)</sup>

isColumnNull(columnIndex: number): boolean

Checks whether the value in the specified column of the current row is null.

> **NOTE**
>
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [isColumnNull](#iscolumnnull9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| columnIndex | number | Yes| Index of the specified column, starting from 0.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the value is null; returns **false** otherwise.|

**Example**

  ```js
  const isColumnNull = resultSet.isColumnNull(resultSet.getColumnIndex("CODES"));
  ```

### close<sup>(deprecated)</sup>

close(): void

Closes this result set.

> **NOTE**
> 
> This API is supported since API version 7 and deprecated since API version 9. You are advised to use [close](#close9).

**System capability**: SystemCapability.DistributedDataManager.RelationalStore.Core

**Example**

  ```js
  let predicatesClose = new dataRdb.RdbPredicates("EMPLOYEE");
  let promiseClose = rdbStore.query(predicatesClose, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
  promiseClose.then((resultSet) => {
      resultSet.close();
  }).catch((err) => {
      console.log('Failed to close the resultset');
  });
  ```
