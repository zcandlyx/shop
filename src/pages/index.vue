<template>
  <div class="index-wrap">
    <div class="index-left">
      <div class="index-left-block">
        <h2>全部产品</h2>
        <template v-for="product in productList">
        <h3>{{product.title}}</h3>
        <ul>
          <li v-for="item in product.list">
            <a :href="item.url">{{item.name}}</a>
            <span v-if="item.hot" class="hot-tag">hot</span>
          </li>
        </ul>
        <div v-if="!product.last" class="hr"></div>
        </template>
      </div>
      <div class="index-left-block lastest-news">
        <h2>最新消息</h2>
        <ul>
          <li v-for="item in newsList">
            <a :href="item.url">{{item.name}}</a>
          </li>
        </ul>
      </div>
    </div>
    <div class="index-right">
<!--       <slide-show :slides="slides"></slide-show> -->
      <div class="index-board-list">
        <div class="index-board-item" v-for="(item, index) in boardList" :class="[{'line-last' : index % 2 !== 0},'index-board-'+item.id]">
          <div class="index-board-item-inner"
            ><h2>{{ item.title }}</h2>
            <p>{{item.description}}</p>
            <div class="index-board-button">
              <a href="" class="button">立即购买</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  created: function () {
    this.$http.post('getList', {userID: 123})
    .then(function (data) {
        console.log(data)
    }, function (err) {
      console.log(err)
    })
  },
  data () {
    return {
        boardList: [
        {
          title: '开放产品',
          description: '开放产品是一款开放产品',
          id: 'car',
          toKey: 'analysis',
          saleout: false
        },
        {
          title: '品牌营销',
          description: '品牌营销帮助你的产品更好地找到定位',
          id: 'earth',
          toKey: 'count',
          saleout: false
        },
        {
          title: '使命必达',
          description: '使命必达快速迭代永远保持最前端的速度',
          id: 'loud',
          toKey: 'forecast',
          saleout: true
        },
        {
          title: '勇攀高峰',
          description: '帮你勇闯高峰，到达事业的顶峰',
          id: 'hill',
          toKey: 'publish',
          saleout: false
        }
      ],
      newsList: [
        {
          name: '奥巴马去世',
          url: 'http://www.baidu.com'
        },
        {
          name: '程序员涨工资了',
          url: 'http://www.baidu.com'
        },
        {
          name: '外星人12月底登陆地球',
          url: 'http://www.baidu.com',
          hot: true
        },
        {
          name: '地球将被外星人接管',
          url: 'http://www.baidu.com'
        }
      ],
      productList: {
        pc: {
          title: 'PC产品',
          list: [
            {
              name: '数据统计',
              url: 'http://www.baidu.com'
            },
            {
              name: '数据预测',
              url: 'http://www.baidu.com'
            },
            {
              name: '流量分析',
              url: 'http://www.baidu.com',
              hot: true
            },
            {
              name: '广告发布',
              url: 'http://www.baidu.com'
            }
          ]
        },
        app: {
          title: '手机APP类',
          last: true,
          list: [
            {
              name: '高德地图',
              url: 'http://www.gaode.com'
            },
            {
              name: 'QQ',
              url: 'http://www.gaode.com',
              hot: true
            },
            {
              name: '微信',
              url: 'http://www.gaode.com'
            },
            {
              name: '淘宝',
              url: 'http://www.gaode.com'
            }
          ]
        }
      }
    }
  }
}
</script>

<style scoped>
.index-wrap {
  width: 1200px;
  margin: 0 auto;
  overflow: hidden;
}
.index-left {
  float: left;
  width: 300px;
  text-align: left;
}
.index-right {
  float: left;
  width: 900px;
}
.index-left-block {
  margin: 15px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
}
.index-left-block .hr {
  margin-bottom: 20px;
}
.index-left-block h2 {
  background: #4fc08d;
  color: #fff;
  padding: 10px 15px;
  margin-bottom: 20px;
}
.index-left-block h3 {
  padding: 0 15px 5px 15px;
  font-weight: bold;
  color: #222;
}
.index-left-block ul {
  padding: 10px 15px;
}
.index-left-block li {
  padding: 5px;
}
.index-board-list {
  overflow: hidden;
}
.index-board-item {
  float: left;
  width: 400px;
  background: #fff;
  box-shadow: 0 0 1px #ddd;
  padding: 20px;
  margin-right: 20px;
  margin-bottom: 20px;
}
.index-board-item-inner {
  min-height: 125px;
  padding-left: 120px;
}
.index-board-car{
  background: url(../assets/images/car.png) no-repeat;
}
.index-board-loud{
  background: url(../assets/images/loud.png) no-repeat;
}
.index-board-earth{
  background: url(../assets/images/earth.png) no-repeat;
}
.index-board-hill{
  background: url(../assets/images/hill.png) no-repeat;
}
.index-board-item h2 {
  font-size: 18px;
  font-weight: bold;
  color: #000;
  margin-bottom: 15px;
}
.line-last {
  margin-right: 0;
}
.index-board-button {
  margin-top: 20px;
}
.lastest-news {
  min-height: 512px;
}
.hot-tag {
  background: red;
  padding:2px 4px;
  color: #fff;
}
.new-item {
  display: inline-block;
  width: 230px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
