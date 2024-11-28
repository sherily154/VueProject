<!-- 语法糖 -->
<script setup>
import {reactive, ref, computed, watch, onMounted, provide} from "vue"; //响应式数据
  import sonVue from "./pages/son.vue";

  //reactive只能接收对象类型的参数
  const state = reactive({
    count: 0,
  })
  //ref可以接收简单和对象类型参数
  const count = ref(0);
  const setCount = () => {
    state.count++;
    count.value++;
  }

  const list = ref([1,2,3,4,5,6,7,8]);
  //计算属性尽量不要修改
  const computedList = computed(() => {
    return list.value.filter(item => item > 2);
  })
  setTimeout(() => {
    list.value.push(9,10);
  },300)

  const name = ref("name")
  const setName = () => {
    name.value = "change";
  }
  //ref不用加.value
  watch([count,name],([newCount,newName],[oldCount,oldName],) => {
    console.log(newCount,oldCount);
    console.log(newName,oldName);
    console.log("count,name变化了")
  },{
    immediate: true,
    deep: true,
  })

  const getMessage = (message) =>{
    console.log(message)
  }

  const h1Ref = ref(null);
  onMounted(() => {
    console.log(h1Ref.value)
  })

  //跨层组件通信 provide  inject
  provide('key',"跨层")


</script>

<template>
  <div>
    <div ref="h1Ref">我是dom标签</div>

    <sonVue @get-massage="getMessage"></sonVue>

    <div>
      原始数组：{{list}}
    </div>
    <div>
      计算数组：{{computedList}}
    </div>
    <button @click="setCount">
      {{state.count}}
    </button>
    <button @click="setName">
      {{name}}
    </button>
  </div>
</template>






<!--<script>-->
<!--  export default {-->
<!--    setup() {-->
<!--      console.log("setup")-->
<!--      const message = "this is a message"-->
<!--      const logMessage = () =>{-->
<!--        console.log(message)-->
<!--      }-->

<!--      return {-->
<!--        message,-->
<!--        logMessage-->
<!--      }-->
<!--    },-->
<!--    beforeCreate() {-->
<!--      console.log("beforeCreate")-->
<!--    }-->
<!--  }-->
<!--</script>-->