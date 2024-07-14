watch props 若是基础数据类型需要getter 

const props = defindProps<{
  data: string
}>()

watch(() => props.data, ()=>{})

类型声明组件ref 可以使用ref泛型ref<typeof VueComponent | null>(null)