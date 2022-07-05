<template>
  <h2>child子组件
  </h2>
  <h3>msg:{{msg}}</h3>
  <button @click="emitData">分发事件</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  beforeCreate(){
    console.log('beforeCreate执行了')
  },
  mounted(){
    console.log('mouted执行了')
  },
  // setup执行在beforecreate之前
  // setup返回值是一个对象 内部的属性方法是给html模板使用
  // setup对象的内部属性和data函数中的return对象的属性都可以在html中使用
  // setup对象中的属性和data函数中的对象中的属性会合并为组件对象的属性
  // setup对象中的方法和methods对象中的方法会合并为组件对象的方法
  // 在vue3中不要混合data和setup、methods和setup - 在methods中可以访问setup提供的属性和方法，但在setup中不能访问data和methods
  setup(props, context){
    // props参数是一个对象，里面有父组件向子组件传递的数据，并且是在子级组件中使用props接收到的所有属性
    console.log('setup执行了')
    console.log(props);
    console.log(context.attrs)
    
    function emitData() {
      context.emit('emitData','emit的数据')
    }
    return {
      emitData
    }
    
  }
});
</script>

