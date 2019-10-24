<template>
  <div class="container">
   
    <div class="quote">
      <!-- <p>
      More information is always better than less. 
      When people know the reason things are happening, even if it's bad news, 
      they can adjust their expectations and react accordingly. 
      Keeping people in the dark only serves to stir negative emotions.<br/>
      - <b>Simon Sinek</b>
    </p> -->
   
    </div>
    
    <div v-if="isLoading" class="spin-class">
      <a-spin>
        <a-icon slot="indicator" type="loading" style="font-size: 50px" spin />
      </a-spin>
    </div>

    <div class="news-container"  v-if="!isLoading">
      <a-tabs defaultActiveKey="Home" @change="callback" forceRender>
        <a-tab-pane key="Home">
           <span slot="tab">
              <a-icon type="home" />
               Home
          </span>
          <div class="card-container">
            <h3>Welcome to acta</h3>
           <p class="about-item">
             Before the invention of newspapers in the early 17th century, official government bulletins and edicts were circulated at times in some centralized empires.
             The first documented use of an organized courier service for the diffusion of written documents is in Egypt, where Pharaohs used couriers for the diffusion of 
             their decrees in the territory of the State (2400 BC). Julius Caesar regularly publicized his heroic deeds in Gaul, and upon becoming dictator of Rome 
             began publishing government announcements called Acta Diurna.(Wikipedia)
           </p>
          </div>
        </a-tab-pane>
        <a-tab-pane key="News" >
           <span slot="tab">
              <a-icon type="global" />
                News
          </span>
          <div class="card-container">
           <news-component v-for="(news, index) in categoryNews" :key="index"
            :link="news.link"
            :summary="news.summary"
            :date="news.date"
            :category="news.category"
            :source="news.source"
            :title="news.title"></news-component>
          </div>
        </a-tab-pane>
        <a-tab-pane key="Business" >
          <span slot="tab">
              <a-icon type="dollar" />
                Business
          </span>
          <div class="card-container">
           <news-component v-for="(news, index) in categoryNews" :key="index"
            :link="news.link"
            :summary="news.summary"
            :date="news.date"
            :category="news.category"
            :source="news.source"
            :title="news.title"></news-component>
          </div>
        </a-tab-pane>
        <a-tab-pane key="Politics" >
          <span slot="tab">
              <a-icon type="bank" />
                Politics
          </span>
          <div class="card-container">
           <news-component v-for="(news, index) in categoryNews" :key="index"
            :link="news.link"
            :summary="news.summary"
            :date="news.date"
            :category="news.category"
            :source="news.source"
            :title="news.title"></news-component>
          </div>
        </a-tab-pane>
        <a-tab-pane key="Entertainment">
          <span slot="tab">
              <a-icon type="shake" />
                Entertainment
          </span>
          <div class="card-container">
           <news-component v-for="(news, index) in categoryNews" :key="index"
            :link="news.link"
            :summary="news.summary"
            :date="news.date"
            :category="news.category"
            :source="news.source"
            :title="news.title"></news-component>
          </div>
        </a-tab-pane>
        <a-tab-pane key="Sports">
          <span slot="tab">
              <a-icon type="dribbble" />
                Sports
          </span>
          <div class="card-container">
           <news-component v-for="(news, index) in categoryNews" :key="index"
            :link="news.link"
            :summary="news.summary"
            :date="news.date"
            :category="news.category"
            :source="news.source"
            :title="news.title"></news-component>
          </div>
        </a-tab-pane>
        <a-tab-pane key="Specials" forceRender>
          <span slot="tab">
              <a-icon type="eye" />
                Specials
          </span>
          <div class="card-container">
           <news-component v-for="(news, index) in categoryNews" :key="index"
            :link="news.link"
            :summary="news.summary"
            :date="news.date"
            :category="news.category"
            :source="news.source"
            :title="news.title"></news-component>
          </div>
        </a-tab-pane>
      </a-tabs>
    </div>

    <!-- <div class="news-container" v-if="!isLoading">
      <news-component v-for="(news, index) in news" :key="index"
        :link="news.link"
        :summary="news.summary"
        :date="news.date"
        :category="news.category"
        :source="news.source"
        :title="news.title"></news-component>
    </div> -->
  </div>
</template>

<script>
//import NavComponent from '~/components/NavComponent.vue'
import NewsComponent from '~/components/NewsComponent.vue'

export default{
  components:{
    //NavComponent,
    NewsComponent
  },
  data(){
    return{
      news: [],
      errors: [],
      isLoading: false,
      categoryNews:[]
    }
  },
  
  methods:{
    loadData:function(){
      this.isLoading = true;
      const URL = 'https://ngnagg.azurewebsites.net/api/ngnews';
      this.$axios.$get(URL)
        .then(response => {
            this.news = response
            this.shuffleArr(this.news)  
            this.isLoading = false
            localStorage.setItem('newsdata', JSON.stringify(this.news))
            //console.log(localStorage.getItem('newsdata'))         
          })
          .catch(e => {
            this.errors.push(e)
            //console.log(this.errors)
          })
    },
    shuffleArr:function(array) {
      array.sort(() => Math.random() - 0.5);
    },
    dataLocalStorage:function(){
      this.news = JSON.parse(localStorage.getItem('newsdata'));
      //console.log(this.news)
    },
    callback(key){
      // this.categoryNews = this.news
      // console.log(this.categoryNews)
      const NEWSDATA = JSON.parse(localStorage.getItem('newsdata'));
      var news = NEWSDATA.filter(function(item){
        return item.category == key
      });

      this.categoryNews = news.sort(() => Math.random() - 0.5);

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
.card-container{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
p{
  font-size: 13px;
  width: 300px;
  text-align: center;
  margin: 10px auto;
}

.about-item{
  text-align: left;
  width: auto;
  margin: auto;
}
.spin-class{
  padding-top: 100px;
  text-align: center;
}

.quote{
  background-color: #E4D9FF;
  padding: 10px;
  background-image: url('https://images.unsplash.com/photo-1495020689067-958852a7765e?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80');
  background-size: cover;
  height: 150px;
  display: flex;
  justify-content: center;
}

@media screen and (min-width: 768px) {
  .quote {
    height: 350px;
  }
}
</style>
