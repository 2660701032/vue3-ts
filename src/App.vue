<template>
  <h2>ref、和toRef、toRefs俩函数
  </h2>
  <h3>ref</h3>
  <p>姓名：{{name_ref}}</p>
  <button @click="btnName">修改信息</button>
  <br>
  <h3>toRef</h3>
  <p>姓名：{{boy_toRef}}</p>
  <p>年龄：{{boy.age}}</p>
  <button @click="btnBoy">修改信息</button>
  <br>
  <h3>toRefs函数</h3>
  <p>姓名：{{name2}}</p>
  <p>年龄：{{age2}}</p>
</template>
<script lang="ts">
import { defineComponent, ref, toRef, toRefs } from 'vue'

export default defineComponent({
  setup() {
    const name = '小明'
    const name_ref = ref(name)
    const btnName = () => {
      name_ref.value = '萧炎'
      // ref代理的数据源没有变还是小明 但ref变成了萧炎
      // ref 函数可以将对象里面的属性值变成响应式的数据，修改响应式数据，是不会影响到源数据，但是视图层上的数据会被更新
      console.log(name, name_ref)
    }

    const boy = {
      name: '我是ed',
      age: 10,
    }
    const boy_toRef = toRef(boy, 'name')
    console.log(boy, boy_toRef)
    const btnBoy = () => {
      boy_toRef.value = '𝒆𝒅'
      // toRef 把源数据boy修改了 但是toRef没有变
      // toRef 函数会与源数据交互，修改响应式数据会造成源数据的修改，但是他的修改不会造成视图层数据的更新
      console.log(boy, boy_toRef)
    }

    const boy2 = {
      name2: '我是ed',
      age2: 10,
    }
    /*
      toRefs 函数用于批量设置多个数据为相应是数据。
      toRefs 函数与原始数据相交互，修改响应式数据会影响到源数据，但是不会更新视图层。
      toRefs 函数还可以与其他响应式数据相交互，更加方便处理视图层数据
      在return中直接...toRefs(boy2) 然后在html模板中就可以解构出boy2中的属性了，但是改变就不能更新视图了。
    */ 
    // const boy_toRefs = toRefs(boy2)
    console.log(boy2)

    return {
      name_ref,
      btnName,
      boy,
      boy_toRef,
      btnBoy,
      // boy2,
      // boy_toRefs,
      ...toRefs(boy2)
    }
  },
})
</script>
