<template>
  <h2>计算属性和监听</h2>
  <fieldset>
    <legend>姓名操作</legend>
    姓氏：<input type="text"  v-model="user.firstName" /> <br>
    名字：<input type="text" v-model="user.lastName" >
  </fieldset>
  <fieldset>
    <legend>计算属性和监听的演示</legend>
    姓名：<input type="text" v-model="fullName1" /> <br>
    姓名：<input type="text"  v-model="fullName2" /> <br>
    姓名：<input type="text" v-model="fullName3">
  </fieldset>
  
</template>
<script lang="ts">
import { computed, defineComponent, reactive, watch, ref, watchEffect } from 'vue'

export default defineComponent({
  setup() {
    const user = reactive({
      firstName: '东方',
      lastName: '不败'
    })
    // 通过计算属性 获得第一个姓名
    // 计算属性中如果只穿入一个回调函数 表示get （简写）
    // 返回的是一个ref类型的对象
    const fullName1 = computed(()=>{
      return user.firstName + '_' + user.lastName
    })

    const fullName2 = computed({
      get(){
        return user.firstName + '_' + user.lastName
      },
      set(val:string){
        console.log(val)
        const names = val.split('_')
        user.firstName = names[0]
        user.lastName = names[1]
      }
    })

    const fullName3 = ref('')
    //  监听 - watch
    // watch(user,({firstName, lastName})=>{
    //   fullName3.value = firstName + '_' + lastName
      
    // },{
    //   immediate: true,
    //   deep: true,
    // })

    // 监听 - 多个数据
    // watch([user.firstName, user.lastName, fullName3],()=>{
    //   // 这里代码没有执行，fullname3是响应式的 而user.firstName, user.lastName不是响应式的
    //   console.log('多个监听了');
    // })
    // 监听 - 监听非响应式的数据的时候
    watch([()=>user.firstName, ()=>user.lastName],(val)=>{
      // 这里代码没有执行，fullname3是响应式的 而user.firstName, user.lastName不是响应式的
      console.log('多个监听了', val);
    })

    // 监听 - watchEffect
    // 不需要配置immediate
    watchEffect(()=>{
      fullName3.value = user.firstName + '_' + user.lastName
    })

    return {
      user,
      fullName1,
      fullName2,
      fullName3
    }
  },
})
</script>
