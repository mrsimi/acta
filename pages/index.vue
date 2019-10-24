<template>
  <div class="container">
    <nav-component></nav-component>
    <div class="quote"><p>
      More information is always better than less. 
      When people know the reason things are happening, even if it's bad news, 
      they can adjust their expectations and react accordingly. 
      Keeping people in the dark only serves to stir negative emotions.
      - <b>Simon Sinek</b>
    </p></div>
    <div class="news-container">
      <news-component v-for="(news, index) in news" :key="index"
        :link="news.link"
        :summary="news.summary"
        :date="news.date"
        :title="news.title"></news-component>
    </div>
  </div>
</template>

<script>
import NavComponent from '~/components/NavComponent.vue'
import NewsComponent from '~/components/NewsComponent.vue'

export default{
  components:{
    NavComponent,
    NewsComponent
  },
  data(){
    return{
      news: [],
      errors: []    
    }
  },
  
  methods:{
    loadData:function(){
      const URL = 'https://ngnagg.azurewebsites.net/api/ngnews';
      this.$axios.$get(URL)
        .then(response => {
            this.news = response
            this.shuffleArr(this.news)  
            localStorage.setItem('data', JSON.stringify(this.news))
            console.log(localStorage.getItem('data'))         
          })
          .catch(e => {
            this.errors.push(e)
            console.log(this.errors)
          })
    },
    shuffleArr:function(array) {
      array.sort(() => Math.random() - 0.5);
    },
    dataLocalStorage:function(){
      this.news = JSON.parse(localStorage.getItem('data'));
      console.log(this.news)
    }
  },

  mounted:function(){
    if(navigator.onLine){
      this.loadData();
    }
    if(!navigator.onLine){
      this.dataLocalStorage();
    }
  }
};
</script>

<style scoped>
.container{
  height: 100vh;
}

.news-container{
  display: flex;
  flex-direction: row;
  justify-content: center;
  flex-wrap: wrap;
  margin: 50px;
}

p{
  font-size: 13px;
  width: 300px;
  text-align: center;
  margin: 10px auto;
}

.news-card{
  border-radius: 10px;
  box-shadow:3px 4px 9px 7px #eee;
  margin: 10px;
}
</style>
