# 针对Vue框架中，computed方法使用注意事项

`computed`方法，作为Vue内置的生命周期函数而存在，可以理解为：之前已经声明过，只需要在使用时覆写，不能在methods里重新声明

```
Method “computed” has type “object” in the component definition. Did you reference the function correctly?
```

```
方法“computed”在组件定义中具有类型“object”。你正确地引用了函数吗？
出现这样的问题就是 将methods方法报裹住了computed

computed: {
        carId() {
            if(this.addForm.goods_cat.length===3){
                return this.addForm.goods_cat[2]
                console.log( this.addForm.goods_cat);
                
            }
            return null
        }
```

