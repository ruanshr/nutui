<template>
  <div class="demo full">
    <h2>基础用法</h2>
    <nut-cell @click="switchActionSheet('dialogShow')">点击出现输出框</nut-cell>
    <nut-cell>您输入的密码是：{{ state.value }}</nut-cell>
    <h2>展示按钮</h2>
    <nut-cell @click="switchActionSheet('dialogShow1')"
      >点击出现输出框</nut-cell
    >
    <nut-cell>您输入的密码是：{{ state.value1 }}</nut-cell>
    <h2>自定义长度</h2>
    <nut-cell @click="switchActionSheet('dialogShow2')"
      >点击出现输出框</nut-cell
    >
    <nut-cell>您输入的密码是：{{ state.value2 }}</nut-cell>
    <h2>出现提示信息</h2>
    <nut-cell @click="switchActionSheet('dialogShow3')"
      >点击出现输出框</nut-cell
    >
    <nut-cell>您输入的密码是：{{ state.value3 }}</nut-cell>
    <nut-shortpassword
      v-model:value="state.value"
      v-model:is-visible="state.dialogShow"
    >
    </nut-shortpassword>
    <nut-shortpassword
      v-model:value="state.value1"
      v-model:is-visible="state.dialogShow1"
      :no-button="false"
      @sureClick="sureClick"
    >
    </nut-shortpassword>
    <nut-shortpassword
      v-model:value="state.value2"
      v-model:is-visible="state.dialogShow2"
      :length="5"
    >
    </nut-shortpassword>
    <nut-shortpassword
      v-model:value="state.value3"
      v-model:is-visible="state.dialogShow3"
      :errorMsg="state.errorMsg"
    >
    </nut-shortpassword>
  </div>
</template>

<script lang="ts">
import { ref, reactive, toRefs, watch } from 'vue';
import { createComponent } from '@/utils/create';
const { createDemo } = createComponent('shortpassword');
export default createDemo({
  setup() {
    const state = reactive({
      dialogShow: false,
      dialogShow1: false,
      dialogShow2: false,
      dialogShow3: false,
      value: '',
      value1: '',
      value2: '',
      value3: '',
      errorMsg: ''
    });
    // 方法
    function switchActionSheet(param) {
      state[`${param}`] = !state[`${param}`];
    }
    function sureClick() {
      state.dialogShow1 = false;
    }
    watch(
      () => state.value3,
      val => {
        if (val.length == 6) {
          state.errorMsg = '请输入正确密码';
        }
      }
    );
    return {
      state,
      switchActionSheet,
      sureClick
    };
  }
});
</script>

<style lang="scss" scoped></style>
