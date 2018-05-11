<style scoped>

.tab_container {
  display: flex;
  flex-direction: row;
  margin-left: 24rpx;
  margin-right: 24rpx;
  margin-top: 36rpx;
  margin-bottom: 36rpx;
  border:2rpx solid #e6e6e6;
  border-radius:42rpx;
  padding:8rpx;
}
.tab_text {
  flex: 1;
  font-size: 34rpx;
  color: #666666;
  text-align: center;
  line-height: 64rpx;
}

.tab_selected {
  border: 2rpx solid #ff0000;
  border-radius: 34rpx;
  background-color: #ff3333;
  color: #ffffff;
}
</style>

<template>
  <view class="tab_container">
    <view @click="tabClick(index)" v-for="(item, index) in tabItems" :key="index"  :class="{'tab_text': true, 'tab_selected': item.isSelected }">{{item.title}}</view>
  </view>
</template>

<script>
export default {
  props: {
    titles: {
      type: Array,
      default: ['头条', '军事', '体育', '娱乐']
    },
    index: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
    }
  },
  computed: {
    tabItems () {
      let result = []
      this.titles.forEach((item, index) => {
        result.push({
          title: item,
          isSelected: index === this.index
        })
      })
      return result
    }
  },
  methods: {
    tabClick (index) {
      this.$emit('tabClick', index)
    }
  }
}
</script>
