# Vue实现界面无痕强制刷新

## 强制刷新

`window.location.reload()`，原生 js 提供的方法；    

`this.$router.go(0)`，vue 路由里面的一种方法；    

这两种方法都可以达到页面刷新的目的，简单粗暴，但是用户体验不好，相当于按 F5 刷新页面，页面的重新载入，会有短暂的白屏。

## 伪造刷新

通过路由跳转的方法刷新，具体思路是点击按钮跳转一个空白页，然后再马上跳回来  

```text
// index.vue 首页
this.$router.replace('/empty')

// empty.vue 空白页
created() {
    this.$router.replace('/')
}
```

当点击刷新按钮时地址栏会有快速的地址切换过程

## 无痕刷新

先在全局组件注册一个方法，用该方法控制 `router-view` 的显示与否，然后在子组件调用；

用 `v-if` 控制 `<router-view></router-view>` 的显示；

provide：全局注册方法；

inject：子组件引用 provide 注册的方法； 

**App.vue：**

```vue
<template>
	<div>
        <router-view v-if="isRoutetAlive"></router-view>
    </div>
</template>

<script>
export default{
    name:'App',
    provide(){//注册一个全局方法
        return{
            reload:this.reload
        }
    },
    data(){
        return{
            isRouterAlive:true
        }
    },
    methods:{
        reload(){//刷新界面
            this.$isRouterAlive = false;
            this.$nextTick(() => {
                this.isRouterAlive = true;
            })
        }
    }
}
</script>
```



**当前组件：**

```vue
<template>
	<div>
        <el-button type="primary" class="btn" @click="refresh">刷新</el-button>
    </div>
</template>

<script>
export default{
    inject:['reload'],//引入方法
    methods:{
        refresh(){
            this.reload(); //调用方法
        }
    }
}
</script>
```

当点击按钮时所有页面重新渲染，体验最好