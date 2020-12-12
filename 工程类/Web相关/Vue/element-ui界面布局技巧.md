# element-ui界面布局技巧

## 引言：element-ui作为一个开源Vue组件，个人感觉方便易用，并且扁平简约的风格很受欢迎。下面对element-ui一些官方文档不甚详细的内容进行补充，方便日后使用。

## el-row布局

```
<el-row></el-row>可以理解为bootstrap中的class=“row”

<el-col></el-col>行   一共分为24栏，通过绑定span属性设置
eg：<el-col :span=12></el-col>

```

## el-table-colum布局  头像

其中img赋予三个属性，value，src，index,通过VUE中的属性响应式绑定

```
<el-tbale-colum>
	<tamplate slot-scope="scope">
		<img :src="url">
		</img>
	</tamplate>

</el-table-colum>

<script>
export default{
	data(){
		return{
			url:
		}
	}
}


</script>



```

