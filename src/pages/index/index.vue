<template>
  <view class="index">
    <view>
      <img src="" alt="">
    </view>
    {{ msg }} <Dongdong />
    <view class="btn">
      <nut-button type="primary" @click="handleClick('text', msg2, true)">点我</nut-button>
    </view>
    <nut-toast :msg="msg2" v-model:visible="show" :type="type" :cover="cover"/>
  </view>
  <nut-cell-group title="基础用法">
    <nut-cell>
      <nut-radio-group v-model="radioVal">
        <nut-radio label="1">选项1</nut-radio>
        <nut-radio disabled label="2">选项2</nut-radio>
        <nut-radio label="3">选项3</nut-radio>
      </nut-radio-group>
    </nut-cell>
    <nut-cell>
      <nut-radio-group v-model="radioVal" text-position="left">
        <nut-radio label="1">选项1</nut-radio>
        <nut-radio disabled label="2">选项2</nut-radio>
        <nut-radio label="3">选项3</nut-radio>
      </nut-radio-group>
    </nut-cell>
    <nut-cell>
      <nut-radio-group v-model="radioVal">
        <nut-radio shape="button" label="1">选项1</nut-radio>
        <nut-radio disabled shape="button" label="2">选项2</nut-radio>
        <nut-radio shape="button" label="3">选项3</nut-radio>
      </nut-radio-group>
    </nut-cell>
  </nut-cell-group>
</template>

<script>
import { reactive, toRefs, ref } from 'vue';
import Taro from '@tarojs/taro'
import { Dongdong } from '@nutui/icons-vue-taro';
export default {
  name: 'Index',
  components: {
    Dongdong
  },
  setup() {
    const radioVal = ref('1');
    const state = reactive({
      msg: '欢迎使用 NutUI4.0 开发小程序',
      msg2: '你成功了～',
      type: 'text',
      show: false,
      cover: false
    });

    const handleClick = (type, msg, cover = false) => {
      Taro.request({
        url: 'https://www.baidu.com',
        data: {
          q: '123'
        },
        success(res) {
          console.log(res)
        }
      })
      state.show = true;
      state.msg2 = msg;
      state.type = type;
      state.cover = cover;
    };

    return {
      radioVal,
      ...toRefs(state),
      handleClick
    }
  }
}
</script>

<style lang="scss">
.index {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
