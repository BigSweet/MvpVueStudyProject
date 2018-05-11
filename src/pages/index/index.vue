<template>
  <div class="container">

          <div>
              <swiper class="swiper" :indicator-dots="indicatorDots"
             :autoplay="autoplay" :interval="interval" :duration="duration" >
              <swiper-item class="swipe_item" v-for="(item,index) in imgUrls">
                <img :src ="item" class ="slide-image" />
              </swiper-item>
           </swiper>



          </div>
           <div style="width : 750rpx">
              <stock-tab-bar class="stock_bar"  :titles="stockTabTitles" :index="currentTabIndex" @tabClick="tabClick"></stock-tab-bar>
      <swiper @change="pageChanged" :current="currentTabIndex" :style="{height: swiperHeight + 'rpx'}">
        <swiper-item >
            <div class='content-list'>
        <block v-for="(item,index) in contentNewsList" :key="index">
          <div class='list-item'>
            <div class='list-item-content'>
              <div class='list-item-left'>
                <img :src="item.thumbnail_pic_s">
              </div>
              <div class='list-item-right'>
                <div class='article-title'>{{item.title}}</div>
                <div class='article-source'>{{item.author_name}}</div>
                <div class='article-editTime'>{{item.date}}</div>
              </div>
            </div>
          </div>
        </block>
      </div>
        </swiper-item>
        <swiper-item >
               <div class='content-list'>
        <block v-for="(item,index) in contentNewsList" :key="index">
          <div class='list-item'>
            <div class='list-item-content'>
              <div class='list-item-left'>
                <img :src="item.thumbnail_pic_s">
              </div>
              <div class='list-item-right'>
                <div class='article-title'>{{item.title}}</div>
                <div class='article-source'>{{item.author_name}}</div>
                <div class='article-editTime'>{{item.date}}</div>
              </div>
            </div>
          </div>
        </block>
      </div>
        </swiper-item>
        <swiper-item >
            <div class='content-list'>
        <block v-for="(item,index) in contentNewsList" :key="index">
          <div class='list-item'>
            <div class='list-item-content'>
              <div class='list-item-left'>
                <img :src="item.thumbnail_pic_s">
              </div>
              <div class='list-item-right'>
                <div class='article-title'>{{item.title}}</div>
                <div class='article-source'>{{item.author_name}}</div>
                <div class='article-editTime'>{{item.date}}</div>
              </div>
            </div>
          </div>
        </block>
      </div>
        </swiper-item>
        <swiper-item >
           <div class='content-list'>
        <block v-for="(item,index) in contentNewsList" :key="index">
          <div class='list-item'>
            <div class='list-item-content'>
              <div class='list-item-left'>
                <img :src="item.thumbnail_pic_s">
              </div>
              <div class='list-item-right'>
                <div class='article-title'>{{item.title}}</div>
                <div class='article-source'>{{item.author_name}}</div>
                <div class='article-editTime'>{{item.date}}</div>
              </div>
            </div>
          </div>
        </block>
      </div>
        </swiper-item>
      </swiper>
           </div>
  </div>
</template>
<script>
var Fly = require('flyio/dist/npm/wx')
import StockTabBar from '@/components/stock-tab-bar'
export default {
  data () {
    return {
      userInfo: {},
      stockTabTitles: ['头条', '军事', '体育', '娱乐'],
      currentTabIndex: 0,
      imgUrls: [
        'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
        'http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg',
        'http://img06.tooopen.com/images/20160818/tooopen_sy_175833047715.jpg'
      ],
      indicatorDots: true,
      autoplay: true,
      interval: 5000,
      duration: 1000,
      contentNewsList: []
    }
  },
  computed: {
    swiperHeight () {
      if (this.contentNewsList && this.contentNewsList.length > 0) {
        return Math.max(this.contentNewsList.length * 180, 750)
      } else {
        return 750
      }
    }
  },
  components: {
    stockTabBar: StockTabBar
  },

  methods: {
    getNewsData: function (type) {
      wx.showLoading({
        title: '加载中',
        mask: true
      })
      let fly = new Fly()
      fly
        .get('https://v.juhe.cn/toutiao/index', {
          type: type,
          key: 'fc35d7872c25744ab4669c7d9dbcf15e'
        })
        .then(res => {
          wx.hideLoading()
          console.log(res)
          this.contentNewsList = res.data.result.data
        })
    },
    tabClick (index) {
      this.currentTabIndex = index
    },
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    pageChanged (event) {
      console.log(this.getitemid())
      var id = this.getitemid()
      this.getNewsData(id)
      this.currentTabIndex = event.mp.detail.current
    },
    getitemid () {
      if (this.currentTabIndex === 0) {
        return 'top'
      } else if (this.currentTabIndex === 1) {
        return 'junshi'
      } else if (this.currentTabIndex === 2) {
        return 'tiyu'
      } else if (this.currentTabIndex === 3) {
        return 'yule'
      }
    }
  },
  created () {
    // 调用应用实例的方法获取全局数据
    this.getNewsData('top')
  }
}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.container{
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
}

.stock_bar {
    width: 750rpx;
    position: flex;
}
.swiper {
  width: 750rpx;
  height: 475rpx;
}

.slide-image {
  width: 750rpx;
  height: 475rpx;
}


.content-list {
  background-color: #fff;
  z-index: 1;
  position: relative;
}
.list-item {
  height: 180rpx;
  width: 100%;
  box-sizing: border-box;
}
.list-item-content {
  padding: 20rpx 30rpx 20rpx 30rpx;
  border-bottom: 1px solid #e5e5e5;
  overflow: hidden;
  box-sizing: border-box;
}
.list-item-left {
  height: 140rpx;
  width: 186rpx;
  margin-right: 20rpx;
  float: left;
}
.list-item-left image {
  width: 100%;
  height: 100%;
}
.list-item-right {
  float: left;
  width: 484rpx;
  height: 140rpx;
  position: relative;
}
.article-title {
  font-size: 14px;
  color: #404040;
  text-align: justify;
  height: 86rpx;
  overflow-y: hidden;
}
.article-source::before {
  content: "作者:";
  font-size: 12px;
  color: #888;
  margin-right: 10rpx;
}
.article-source {
  font-size: 12px;
  color: #888;
  position: absolute;
  bottom: 0;
  right: 0;
}
.article-editTime {
  font-size: 12px;
  color: #a8a8a8;
  position: absolute;
  bottom: 0;
  left: 0;
}
</style>
