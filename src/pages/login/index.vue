<template lang='pug'>
.login-container
    .login-logo
    button.login-btn(open-type='getUserInfo' lang='zh-CN' @getuserinfo='doLogin') 微信授权

</template>
<script>
import {host} from '../../utils'
var qcloud = require('wafer2-client-sdk/index.js')
console.log(qcloud)
export default {
  data () {
    return {

    }
  },
  mounted () {
    console.log(host)
    qcloud.setLoginUrl(host + '/weapp/login')
  },
  methods: {
    doLogin () {
      wx.showLoading({
        title: '登录中....',
        mask: true,
        success: res => {}
      })
      const session = qcloud.Session.get()
      if (session) {
        // 第二次登录，或者本地已经有登录态
        // 可使用本函数更新登录态
        qcloud.loginWithCode({
          success: res => {
            console.log(res)
            wx.setStorageSync('key', 'value')
            wx.hideLoading()
            wx.navigateBack({})
          },
          fail: err => {
            console.log(err)
            wx.hideLoading()
            wx.navigateBack({})
          }
        })
      } else {
        // 首次登录
        qcloud.login({
          success: res => {
            console.log(res)
            wx.hideLoading()
            wx.setStorageSync('userInfo', res)
            var openId = res.openId
            wx.setStorageSync('openId', openId)
            // 返回上一级
            wx.navigateBack({})
          },
          fail: err => {
            console.log(err + 'err')
            wx.hideLoading()
            // 返回上一级
            wx.navigateBack({})
          }
        })
      }
    }

  }
}
</script>
<style lang="scss">
.login-container{
    width: 100%;
    height: 100%;
    background: #fff;
    box-sizing: border-box;
    padding-top: 1rpx;
    .login-logo{
        width: 230rpx;
        height: 80rpx;
        background: url('../../../static/images/logo1.png') no-repeat;
        background-size: 100% 100%;
        margin: 200rpx auto 0 auto;
    }
    .login-btn{
        text-align: center;
        background-color: #b4a078;
        width: 90%;
        height: 80rpx;
        line-height: 80rpx;
        color: #fff;
        font-size: 28rpx;
        margin-top: 300rpx;
    }

}
    
</style>