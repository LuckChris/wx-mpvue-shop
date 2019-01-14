<template lang='pug'>
.user-center-container
  .user-center-top
    .avator-img
      img(:src='avator' @click='goToLogin')
    .content(@click='goToLogin')
      template(v-if='showLoginTitle')
        p 未登录
        p 点击登录账号
      template(v-else)
        p {{nickname}}  
  .icon-list
      .icon-item(v-for="(item,index) in listDate" @click='goTo(item.path)' :key="index")
        i.iconfont(:class='item.icon')
        span {{item.title}}   
</template>
<script>
export default {
  data () {
    return {
      avator: 'http://yanxuan.nosdn.127.net/8945ae63d940cc42406c3f67019c5cb6.png',
      listDate: [
        {
          title: '我的订单',
          icon: 'icon-dingdan',
          path: '/pages/order/main'
        },
        {
          title: '我的拼团',
          icon: 'icon-tuangou',
          path: ''
        },
        {
          title: '我的收藏',
          icon: 'icon-star',
          path: ''
        },
        {
          title: '我的积分',
          icon: 'icon-jifen',
          path: ''
        },
        {
          title: '退款/售后',
          icon: 'icon-shouhou',
          path: ''
        },
        {
          title: '优惠券',
          icon: 'icon-youhuiquan',
          path: ''
        },
        {
          title: '红包',
          icon: 'icon-hongbao',
          path: '/pages/red-packet/main'
        },
        {
          title: '礼品卡',
          icon: 'icon-lipinqia',
          path: ''
        },
        {
          title: '地址管理',
          icon: 'icon-address',
          path: ''
        },
        {
          title: '账号安全',
          icon: 'icon-anquan',
          path: ''
        },
        {
          title: '联系客服',
          icon: 'icon-liaotian',
          path: ''
        },
        {
          title: '用户反馈',
          icon: 'icon-fankui',
          path: ''
        },
        {
          title: '帮助中心',
          icon: 'icon-bangzhu',
          path: '/pages/help/main'
        }
      ],
      nickname: '',
      showLoginTitle: true
    }
  },
  onShow () {
    let userInfo = wx.getStorageSync('userInfo')
    this.showLoginTitle = !userInfo
    if (userInfo) {
      this.avator = userInfo.avatarUrl
      this.nickname = userInfo.nickName
    }
  },
  methods: {
    goTo (url) {
      if (url) {
        wx.navigateTo({
          url: url
        })
      } else {
        wx.showModal({
          title: '提示',
          content: '此页面内容还在开发中',
          showCancel: false,
          confirmText: '知道了',
          success (res) {
            if (res.confirm) {
              console.log('用户点击确定')
            }
          }
        })
      }
    },
    goToLogin () {
      if (!this.userInfo) {
        wx.navigateTo({
          url: '/pages/login/main'
        })
      }
    }
  },
  mounted () {

  }
}
</script>
<style lang="scss">
.user-center-container{
  width: 100%;
  height: 100%;
  color: #333;
  font-size: 28rpx;
  .user-center-top{
    width: 100%;
    height: 300rpx;
    background-color: #e3ce9c;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    padding: 0 30rpx;
    .avator-img{
      width: 120rpx;
      height: 120rpx;
      border-radius: 50%;
      overflow: hidden;
      margin-right: 30rpx;
    }
    img{
      width: 120rpx;
      height: 120rpx;
    }
    .content{
      p:first-child{
        font-size: 30rpx;
      }

    }
  }
  .icon-list{
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    text-align: center;
    background-color: #fff;
    .icon-item{
      width: 33.33%;
      padding: 50rpx 0;
      border-right: 1rpx solid #d9d9d9;
      border-bottom: 1rpx solid #d9d9d9;
      box-sizing: border-box;
      i{
        font-size: 60rpx;
        display: block;
      }
      span{
        font-size: 30rpx;
      }
      &:nth-child(3n + 3) {
        border-right: none;
      }
      &:last-child{
        border-bottom: none;
      }
    }
  }
}
    
</style>
