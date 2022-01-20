<template>
  <div class="main1">
    <h1>{{ msg }}</h1>
    <h1>{{ roadpart }}</h1>
    <button @click="add">点击</button>
    <div v-html="strhtml"></div>
  </div>
</template>



<script>
// mounted 钩子函数  这里去请求豆瓣数据

export default {
  name: 'home',
  data () {
    return {
      msg: '路段信息',
      articles:[],
      roadpart: 0,
      strhtml:""
    }
  },
  created:function(){  //这里mounted和created生命周期函数区别
     this.$http.jsonp('https://api.douban.com/v2/movie/top250?count=10', {}, {
        headers: {

        },
        emulateJSON: true
    }).then(function(response) {
      // 这里是处理正确的回调
        console.log(response);
        this.articles = response.data.subjects
        // this.articles = response.data["subjects"] 也可以

    }, function(response) {
        // 这里是处理错误的回调
        console.log(response)
    });
  },
  mounted: function(){
      // console.log(this.$route.query)
      // let q = this.$route.query
      // this.roadpart = q.id
      
  },
  watch: {
    '$route' (to, from) {
        console.log(this.$route.query)
        let q = this.$route.query
        this.roadpart = q.id
    }
  },
  methods: {
    add(){
      //this.counter.push({});
      this.strhtml = '<img src="/static/car_1_1.png" style="left:283px;position: relative;"></img><img src="/static/car_1_1.png" style="left:383px;position: relative;"></img>'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul{
  list-style: none;
  margin: 0;
  padding: 0;
}
ul li{
border-bottom: 1px solid #999;
padding: 10px 0;
}

.inl-block{
display: inline-block;
}

.m-img{
  
}
.m-content{
margin-left: 20px;
}

.main1 {
    width: 2000px;
    height: 600px;
    background: url('/static/road.png');
  }
</style>
