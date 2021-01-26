## IndexDB数据库

使用IndexedDB的第一步是打开数据库，使用indexedDB.open()方法。

let request = window.indexedDB.open(databaseName, version);

这个方法接受两个参数，第一个参数是字符串，表示数据库的名字。如果指定的数据库不存在，就会新建数据库。第二个是整数，表示数据库的版本。如果省略，打开已有数据库时默认为当前版本；新建数据库时，默认为1。

返回一个IDBRequest对象。这个对象通过三种事件error、success、upgradeneeded,处理打开数据库的操作结果。

