<template>
  <div></div>
  <div>{{ count }}</div>
  <span v-pre>{{ this will not be compiled }}</span>
  <div>{{ num }}</div>
  <!-- <div>姓名：{{ obj.name }}</div>
  <div>性别：{{ obj.sex }}</div>
  <div>年龄：{{ obj.age }}</div> -->
  <div>姓名：{{ name }}</div>
  <div>性别：{{ sex }}</div>
  <div>年龄：{{ age }}</div>
  <button @click="countAdd">操作</button>
</template>
<script>
import {} from "vue";
import {
  ref,
  reactive,
  toRefs,
  onBeforeMount,
  onMounted,
  onRenderTriggered,
  onRenderTracked,
} from "vue";
export default {
  beforeCreate() {
    console.log("----beforeCreate----");
  },
  created() {
    console.log("----created----");
  },
  setup() {
    console.log("----setup----");
    // vue3.x生命周期写在setup中
    onBeforeMount(() => {
      console.log("------onBeforeMount-----");
    });
    onMounted(() => {
      console.log("------onMounted-----");
    });
    // 调试哪些数据发生了变化
    onRenderTriggered((event) => {
      console.log("------onRenderTriggered-----", event);
    });
    onRenderTracked((event) => {
      console.log("------onRenderTracked-----", event);
    });
    let { count, obj, countAdd } = countAddModal();
    console.log(count, obj, countAdd);
    return { count, ...toRefs(obj), countAdd };
  },
  data() {
    return {
      num: 2333,
    };
  }
};
// 将这一块可以看做是一个模块
function countAddModal() {
  // 一般针对简单的数据
  let count = ref(0);
  // 一般创建动态响应的复杂的数据结构比如对象、数字
  let obj = reactive({
    name: "张三",
    sex: "不详",
    age: 0,
  });

  function countAdd() {
    count.value = count.value + 1;
    obj.age = obj.age + 1;
  }
  return { count, obj, countAdd };
}
</script>
<style lang="less">
</style>