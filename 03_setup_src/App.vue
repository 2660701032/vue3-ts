<template>
  <h2>App父组件</h2>
  <h3>mag:{{msg}}</h3>
  <hr />
  <!-- 3.使用子组件 -->
  <child :msg="msg" @emitData="emitData" msg2="真香"></child>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
// 1.引入子组件
import Child from './components/Child.vue'
export default defineComponent({
  name: 'App',
  // 2. 注册子组件
  components: {
    Child
  },
  setup() {
    const msg = ref('what are you no sha lai')
    function emitData (va:string) {
      console.log(va);
      
    }
    return {
      msg,
      emitData
    }
  }
});
</script>

