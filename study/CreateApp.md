## CreateApp

创建应用

之前Vue2

```
new Vue({
    el: '#app',
    router,
    store,
    render: h => h(App)
})
```

现在Vue3:

使用createApp返回一个提供应用上下文的应用实例。应用实例挂载的整个组件树共享同一个上下文。

```
createApp(App).use(store).use(router).mount('#app')
```

可以在其后链式调用其他方法，主要有一下几种：

| 参数                  | 用法                                                         |
| --------------------- | ------------------------------------------------------------ |
| config（配置）        | 包含应用配置的对象。同Vue2中config。提供统一配置。           |
| directive（指令）     | 注册或检索全局指令。指令是一组具有生命周期的钩子。           |
| mixin（混入）         | 在整个应用范围内应用混入。一旦注册，它们就可以在当前的应用中任何组件模板内使用它。插件作者可以使用此方法将自定义行为注入组件。**不建议在应用代码中使用**。 |
| mount（挂载）         | 应用实例的根组件挂载在提供的 DOM 元素上。同Vue2中的el。      |
| provide（搭配Inject） | 设置一个可以被注入到应用范围内所有组件中的值。组件应该使用 `inject` 来接收 provide 的值。从 `provide`/`inject` 的角度来看，可以将应用程序视为根级别的祖先，而根组件是其唯一的子级。该方法不应该与 [provide 组件选项](https://v3.cn.vuejs.org/api/options-composition.html#provide-inject)或组合式 API 中的 [provide 方法](https://v3.cn.vuejs.org/api/composition-api.html#provide-inject)混淆。虽然它们也是相同的 `provide`/`inject` 机制的一部分，但是是用来配置组件 provide 的值而不是应用 provide 的值。通过应用提供值在写插件时尤其有用，因为插件一般不能使用组件提供值。这是使用 [globalProperties](https://v3.cn.vuejs.org/api/application-config.html#globalProperties) 的替代选择。<br />`provide` 和 `inject` 绑定不是响应式的。 |
| unmount（卸载）       | 在提供的 DOM 元素上卸载应用实例的根组件。                    |
| use（使用）           | 安装 Vue.js 插件。在同一个插件上多次调用此方法时，改插件将仅安装一次。 |
| component（组件）     | 注册或检索全局组件。注册还会使用给定的 `name` 参数自动设置组件的 `name`。 |
