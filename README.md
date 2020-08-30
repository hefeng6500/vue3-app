# vue3-app

### v-model 指令

```
// vue 2.x
<ant-input v-model="inputValue"></ant-input>

// vue 3.x
<ant-input v-model:inputValue="inputValue"></ant-input>

```

v-model 指令在 vue 2.x 和 vue 3.0 存在一些差别

- 2.x 中 v-model 语法糖底层使用的是 :value 和 emit('input')， 绑定属性值是 value
- 3.0 中可以绑定一个自定义值，:value="firstName" 和 @input="$emit('update:firstName', $event.target.value)"
- 添加自定义修饰符 v-model.capitalize 

### setup 函数

- 只执行一次
- 优先于 created 执行
- props 父组件传入的属性
- context ：slots、attr、emit

```
setup(props, context){
	onMounted(()=>{
		return <h1>Hello World!</h1>
	})
}
```



### reactive 函数

- 创建响应式的对象
- 

```vue
import { reactive } from 'vue';

const state = reactive({
	selectedKeys: []
})

return {
	state
}
```

### ref  函数

- 单独将某个属性变成响应式
- 当ref作为渲染上下文的属性返回并在模板中进行访问时，它将自动解构为内部值。无需`.value`在模板中追加：

```js
const allTime = ref(store.getters.allTime)

return {
    allTime
}
```

### toRefs 函数

- 对传入的对象进行响应式

```js
import { toRefs } from 'vue';

return {
	...refs(state)
}
```

### watch 函数

```js
const route = useRoute()

watch(()=> route.path, newValue => {
	state.seletctedKeys = [newValue]
})
```

### computed  函数

```js
const seletctedKeys = computed(()=>{
    return [route.path]
})
```


