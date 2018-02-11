---
title: "Vue Lifecycle Hooks"
date: 2018-02-11T00:28:11-05:00
tags: ["VueJs"]
draft: false

---

#### **VueJS Lifecycle Hooks Overview**

Vue Lifecycle is one of the most fundamental yet often ignored concepts for Vue beginner. We will got through some 
examples and source code today to better understand the lifecycle of vue. 

Lifecycle hooks is a place in vue execution process that allows us to add our own code using basic javascript
feature, callback. Let's take a look at the source code on how its implemented.


```javascript
export function lifecycleMixin (Vue: Class<Component>) {
  Vue.prototype._update = function (vnode: VNode, hydrating?: boolean) {
    const vm: Component = this
    if (vm._isMounted) {
      callHook(vm, 'beforeUpdate') // calls beforeUpdate hook
    }
// ...

export function callHook (vm: Component, hook: string) {
  const handlers = vm.$options[hook]
  if (handlers) {
    for (let i = 0, j = handlers.length; i < j; i++) {
      try {
        handlers[i].call(vm)
      } catch (e) {
        handleError(e, vm, `${hook} hook`)
      }
    }
  }
  if (vm._hasHookEvent) {
    vm.$emit('hook:' + hook)
  }
}
```

We can see that the process is executed callHook() after the corresponding process in the life cycle process. 
CallHook performs user-defined functions, the hook refers to the current component instance by 
using Function.prototype.call.

Below is a graph from `VueJS.org` explaining the execution order in more details.

![Vue Lifecyle Image](https://vuejs.org/images/lifecycle.png)


Copy the following code location and open Chrome console to see execution the result.
```javascript
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <script type="text/javascript" src="https://cdn.jsdelivr.net/vue/2.1.3/vue.js"></script>
  </head>
  <body>
    <div id="app">
      <p>{{ message }}</p>
    </div>
    <script type="text/javascript">
      var app = new Vue({
        el: '#app',
        data: {
          message: "Vue Lifecycle"
        },
        beforeCreate: function() {
          console.group('beforeCreate ===============�');
          console.log("%c%s", "color:red", "el     : " + this.$el); //undefined
          console.log("%c%s", "color:red", "data   : " + this.$data); //undefined 
          console.log("%c%s", "color:red", "message: " + this.message)
        },
        created: function() {
          console.group('created ===============�');
          console.log("%c%s", "color:red", "el     : " + this.$el); //undefined
          console.log("%c%s", "color:red", "data   : " + this.$data); //initalized 
          console.log("%c%s", "color:red", "message: " + this.message); //initalized
        },
        beforeMount: function() {
          console.group('beforeMount ===============�');
          console.log("%c%s", "color:red", "el     : " + (this.$el)); //initalized
          console.log(this.$el);
          console.log("%c%s", "color:red", "data   : " + this.$data); //initalized  
          console.log("%c%s", "color:red", "message: " + this.message); //initalized  
        },
        mounted: function() {
          console.group('mounted ===============�');
          console.log("%c%s", "color:red", "el     : " + this.$el); //initalized
          console.log(this.$el);
          console.log("%c%s", "color:red", "data   : " + this.$data); //initalized
          console.log("%c%s", "color:red", "message: " + this.message); //initalized 
          this._data.message = 'updated message under data!!!';
        },
        beforeUpdate: function() {
          console.group('beforeUpdate ===============�');
          console.log("%c%s", "color:red", "el     : " + this.$el);
          console.log(this.$el);
          console.log("%c%s", "color:red", "data   : " + this.$data);
          console.log("%c%s", "color:red", "message: " + this.message);
          
        },
        updated: function() {
          console.group('updated ===============�');
          console.log("%c%s", "color:red", "el     : " + this.$el);
          console.log(this.$el);
          console.log("%c%s", "color:red", "data   : " + this.$data);
          console.log("%c%s", "color:red", "message: " + this.message);
          this.$destroy();
        },
        beforeDestroy: function() {
          console.group('beforeDestroy ===============�');
          console.log("%c%s", "color:red", "el     : " + this.$el);
          console.log(this.$el);
          console.log("%c%s", "color:red", "data   : " + this.$data);
          console.log("%c%s", "color:red", "message: " + this.message);
        },
        destroyed: function() {
          console.group('destroyed ===============�');
          console.log("%c%s", "color:red", "el     : " + this.$el);
          console.log(this.$el);
          console.log("%c%s", "color:red", "data   : " + this.$data);
          console.log("%c%s", "color:red", "message: " + this.message)
        }
      })
    </script>
  </body>
</html>
```
#### **Chrome Console Output**
```javascript
test.html:18 beforeCreate ===============
test.html:19 el     : undefined
test.html:20 data   : undefined
test.html:21 message: undefined
test.html:24 created ===============
test.html:25 el     : undefined
test.html:26 data   : [object Object]
test.html:27 message: Vue Lifecycle
test.html:30 beforeMount ===============
test.html:31 el     : [object HTMLDivElement]
test.html:32 <div id=​"app">​…​</div>​
test.html:33 data   : [object Object]
test.html:34 message: Vue Lifecycle
test.html:37 mounted ===============
test.html:38 el     : [object HTMLDivElement]
test.html:39 <div id=​"app">​…​</div>​
test.html:40 data   : [object Object]
test.html:41 message: Vue Lifecycle
test.html:45 beforeUpdate ===============
test.html:46 el     : [object HTMLDivElement]
test.html:47 <div id=​"app">​…​</div>​
test.html:48 data   : [object Object]
test.html:49 message: updated message under data!!!
test.html:53 updated ===============
test.html:54 el     : [object HTMLDivElement]
test.html:55 <div id=​"app">​…​</div>​
test.html:56 data   : [object Object]
test.html:57 message: updated message under data!!!
test.html:61 beforeDestroy ===============
test.html:62 el     : [object HTMLDivElement]
test.html:63 <div id=​"app">​…​</div>​
test.html:64 data   : [object Object]
test.html:65 message: updated message under data!!!
test.html:68 destroyed ===============
test.html:69 el     : [object HTMLDivElement]
test.html:70 <div id=​"app">​…​</div>​
test.html:71 data   : [object Object]
test.html:72 message: updated message under data!!!
```

#### **Create vs Mount**

**`beforeCreate`**

After Vue Instance and Component created，but before data observer and event/watcher.
Both `el` and `data` are undefined.

**`created`**

`data` is accessible，but DOM has not been created，also `el` is still undefined。


**`beforeMount`**

Both `el` and `data` have been initialized. We can in the console that `{{message}}` under `<div id="app">`，Vue uses 
`Virtual DOM`, so it create a placeholder for the data in the DOM, and only renders it after `mounted`.

**`mounted`**

`el` is replaced by `vm.$el`, and mounted onto instance.

#### **Update**

**`beforeUpdate`**
When we updated `data` in `this._data.message = 'updated message under data!!!';` It automatically invokes
`beforeUpdate` but before virtual DOM is re-rendered.

**`updated`**
Re-renders virtual DOM, and view is presented on the page.

**`activated`**
TODO

**`deactivated`**
TODO

**`beforeDestroy`**
When we call `this.$destroy();` function. It destroys the Vue instance, and Vue no longer respond to any requests to 
update `message`, but the original DOM elements still exist on the page.


**`destroyed`**
TODO


