## Vue 将子组件Value传递给父组件



**引言：**

在进行App制作过程中，由于某个控件需要进行跨界面传输value，由于对于Vue的特性掌握不够熟练而无从下手，现整理在下面。





这里，在另一个页面通过`ref`标识指明该子组件的名称，其后便可以调用子组件的方法。

```vue
<simplify v-show="checked" ref="simple"></simplify>


<script lang="javascript">
export default{
    methods:{
        stopPlay() {
      // 调用子组件的暂停播放
      this.$refs.simple.stopPlay();
    },
    }
}

</script>

```

