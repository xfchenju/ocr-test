<template>
  <div class="index">
    <div class="index-container">
      <h2>身份验证</h2>
      <van-cell-group>
        <van-field
          :value="name"
          placeholder="请输入真实姓名"
        />
        <van-field
          :value="idNumber"
          placeholder="请输入身份证号"
          :border="false"
        />
      </van-cell-group>
      <van-radio-group :value="from" checked-color="#07c160">
        <van-radio name="1">本市户籍</van-radio>
        <van-radio name="2">非本市户籍</van-radio>
      </van-radio-group>
      <camera
        device-position="back"
        flash="off"
        @error="error"
        style="width: 100%; height: 300px;"
        v-if="!imgSrc"
      ></camera >
      <img :src="imgSrc ? imgSrc : null" alt="" v-else>
      <van-button custom-class="identify-btn" type="default" @click="takePhoto">{{imgSrc ? '重新识别' : '识别'}}</van-button>
      <!--<van-button custom-class="next-step-btn" type="primary">下一步</van-button>-->
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      imgSrc: null,
      name: null,
      idNumber: null,
      from: 1
    }
  },
  methods: {
    takePhoto() {
      if(this.imgSrc) {
        this.imgSrc = null;
      }else {
        let _this = this;
        const ctx = wx.createCameraContext()
        ctx.takePhoto({
          quality: 'high',
          success: (res) => {
            _this.imgSrc = res.tempImagePath;
            _this.name = '张三';
            _this.idNumber = '330483199401186666';
          }
        })
      }
    },
    error(e) {
      console.log(e.detail)
    }
  },

  created () {
    // let app = getApp()
  }
}
</script>

<style lang="less">
  .index {
    background: #f5f5f5;
    .index-container {
      padding: 20px;
      border-radius: 5px;
      background: #fff;
    }
  }
  .identify-btn {
    border-color: red !important;
  }
  .next-step-btn {
    width: 80%;
    border-color: red !important;
    background: red !important;
  }
</style>
