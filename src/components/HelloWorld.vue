<template>
  <input type="text" v-model="input" />
  <button @click="addClick">add</button>
  {{ count }}
  <h1>{{ test }}</h1>
  <ul class="panel">
    <li v-for="(item, index) in list" :key="index">
      <div class="title">{{ item.title }}</div>
      <div class="del" @click="delClick(index)">删除</div>
    </li>
  </ul>
</template>

<script>
import { reactive, ref, toRefs, watch, watchEffect } from "vue";
export default {
  setup() {
    const state = reactive({
      list: [
        {
          title: "Ant Design Title 1",
        },
        {
          title: "Ant Design Title 2",
        },
        {
          title: "Ant Design Title 3",
        },
        {
          title: "Ant Design Title 4",
        },
      ],
      input: "",
      count: 0,
    });

    const addClick = function () {
      state.list.push({
        title: state.input,
      });
    };

    const delClick = function (index) {
      state.list.splice(index, 1);
    };

    // let count = ref(0);
    // watch(count, (count, prevCount) => {
    //   console.log("watch count", count);
    // });

    // let test = 123;

    // setTimeout(() => {
    //   count.value++;
    // }, 1000);

    watch(
      () => state.list,
      (list) => {
        console.log(list);
      },
      {
        deep: true,
      }
    );

    const count = ref(0);

    watchEffect(() => console.log(count.value));

    setTimeout(() => {
      count.value++;
    }, 100);

    return {
      ...toRefs(state),
      count,
      // test,
      addClick,
      delClick,
    };
  },
};
</script>

<style scoped>
.panel {
  width: 200px;
}
.title {
  float: left;
}
.del {
  float: right;
  cursor: pointer;
}
</style>
