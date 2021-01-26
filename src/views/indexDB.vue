<template>
<div class="about">
    <h1>学习IndexDB</h1>
    <div @click="openDB">打开数据库</div>
    <div @click="addDB">添加数据</div>
    <div @click="readDB">阅读数据</div>
    <div @click="readAll">阅读所有数据</div>
    <div @click="update">更新数据</div>
    <div @click="remove">删除数据</div>
</div>
</template>

<script>
let db = null;
export default {
    name: "Index",
    data() {
        return {
            data: '1'
        }
    },
    mounted() {

    },
    methods: {
        remove() {
            let request = db.transaction(['person'], 'readwrite')
                .objectStore('person')
                .delete(1);

            request.onsuccess = function (event) {
                console.log(event);
                console.log('数据删除成功');
            };
        },
        openDB() {
            let req = window.indexedDB.open('im', 1);
            console.log(req);
            req.onerror = function (e) {
                console.log(e);
            };
            req.onsuccess = function (event) {
                db = req.result;
                console.log('数据库打开成功');
                console.log(event);
            };
            req.onupgradeneeded = function (event) {
                db = event.target.result;
                console.log(111);
                let objectStore;
                if (!db.objectStoreNames.contains('person')) {
                    objectStore = db.createObjectStore('person', {
                        keyPath: 'id',
                        autoIncrement: true
                    });
                    objectStore.createIndex('name', 'name', {
                        unique: false
                    });
                    objectStore.createIndex('email', 'email', {
                        unique: true
                    });
                }
            }
        },
        readDB() {
            let transaction = db.transaction(['person']);
            let objectStore = transaction.objectStore('person');
            let request = objectStore.get(1);

            request.onerror = function (event) {
                console.log(event);
                console.log('事务失败');
            };

            request.onsuccess = function (event) {
                console.log(request);
                console.log(event);
                if (request.result) {
                    console.log('Name: ' + request.result.name);
                    console.log('Age: ' + request.result.age);
                    console.log('Email: ' + request.result.email);
                } else {
                    console.log('未获得数据记录');
                }
            };
        },
        update() {
            let request = db.transaction(['person'], 'readwrite')
                .objectStore('person')
                .put({
                    id: 1,
                    name: '李四',
                    age: 35,
                    email: 'lisi@example.com'
                });

            request.onsuccess = function (event) {
                console.log(event);
                console.log('数据更新成功');
            };

            request.onerror = function (event) {
                console.log(event);
                console.log('数据更新失败');
            }
        },
        readAll() {
            let objectStore = db.transaction('person').objectStore('person');

            objectStore.openCursor().onsuccess = function (event) {
                let cursor = event.target.result;

                if (cursor) {
                    console.log('Id: ' + cursor.key);
                    console.log('Name: ' + cursor.value.name);
                    console.log('Age: ' + cursor.value.age);
                    console.log('Email: ' + cursor.value.email);
                    cursor.continue();
                } else {
                    console.log('没有更多数据了！');
                }
            };
        },
        addDB() {
            let request = db.transaction(['person'], 'readwrite')
                .objectStore('person')
                .add({
                    id: 1,
                    name: '张三',
                    age: 24,
                    email: 'zhangsan@example.com'
                });

            request.onsuccess = function (event) {
                console.log(event);
                console.log('数据写入成功');
            };

            request.onerror = function (event) {
                console.log(event);
                console.log('数据写入失败');
            }
        }
    }
}
</script>

<style lang="scss" scoped>
    
</style>
