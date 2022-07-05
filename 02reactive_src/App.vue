<template>
  <h2>reactive的使用</h2>
  <h3>名字：{{user.name}}</h3>
  <h3>年龄：{{user.age}}</h3>
  <h3>媳妇：{{user.wife}}</h3>
  <button @click="updateCount">更新数据</button>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';

export default defineComponent({
  name: 'App',

  setup() {
    const obj:any = {
      name: '小明',
      age: 20,
      wife: {
        name: '小甜甜',
        age: 20,
        cars: ['bens', 'bwm', '奥迪']
      }
     }
     const user = reactive(obj)

     const updateCount = () => {
      console.log(user)
      user.name = '小红'
      // user.habby = '钓鱼'
      delete user.age
     }
     return {
      user,
      updateCount
     }
  }
});
</script>

