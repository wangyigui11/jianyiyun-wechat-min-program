<template>
  <div class="user">
    <!-- 用户信息区域 -->
    <Button
      class="weui-btn weui-btn_primary"
      open-type="getUserInfo"
      @getuserinfo="getUserInfo"
    >点击获取用户信息</Button>
    <button
      class="weui-btn weui-btn_primary"
      open-type="getPhoneNumber"
      bindgetphonenumber="getPhoneNumber"
    >获取手机号码</button>
    <button class="weui-btn weui-btn_primary bindtap='getOpenid'">获取openid</button>
    <button type="primary" bindtap="getOpenid">获取用户openid</button>
    <text>{{openid}}</text>
    <!-- <Button  class="weui-btn weui-btn_primary " open-type="getPhoneNumber" bindgetphonenumber="getphonenumber" >获取用户手机号</Button> -->
    
  
  
  </div>
</template>

<script>
export default {
  data() {
    return {
      userInfo: {}
    }
  },
  // DOM创建之前 获得这个数据
  beforeMount() {
    this.userLogin()
  },
  methods: {
    // 同步代码  执行用户登录操作
    async userLogin() {
      let start = Date.now()
      const res = await wx.login()
      if(res.code){
        //如果res.code存在， 发送后台请求
        console.log(res.code);
        console.log('有code，发送ajax请求，获取数据');
      }
      let end = Date.now()
      // console.log(res);
      console.log(end - start);
      
      
    },

    // 获取用户信息

    // 获取用户信息
    handleGetUserInfo() {
      wx.getUserInfo({
        success: data => {
          // 查看成功获取信息的数据data
          console.log('我拿到了 userInfo')
          console.log(data)
          withCredentials: true
          this.userInfo = data.userInfo
          // this.isShow = true
        },
        fail: () => {
          console.log('获取失败------重新获取用户信息')
        }
      })
    },
    // 获取用户信息
    getUserInfo(data) {
      // 判断用户是否授权
      if (data.mp.detail.rawData) {
        // 用户授权 执行下面的操作
        this.handleGetUserInfo()
      }
    },
    // 获取用户的电话号码
    getPhoneNumber(e) {
      console.log(e.detail.errMsg)
      console.log(e.detail.iv)
      console.log(e.detail.encryptedData)
    },
    // userLogin(){
    //   wx.login({
    //   success(res){
    //       console.log('登陆成功');
    //       console.log(res);
    //       let end = Date.now()
    //       console.log("时间",end - start);
    //   },
    //   fail(e) {
    //     console.log('fail: ', e);
    //   }
    // })}

    
  }
}
</script>

<style>
</style>
