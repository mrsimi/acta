<template>
  <a-card :bordered="false" style="width: 250px" class="news-card">
        <h3>{{ title }}}</h3>
        <p>{{ summary|truncate }}</p>
        <a :href="link"> Read More </a> <br/> <br/>
        <a-tag color="#808F85">{{ source }}</a-tag>
    </a-card>
</template>

<script>
export default {
    props: ['title', 'link', 'summary', 'date', 'category', 'source'],
    filters:{
        truncate: function(value){
        if(value.length > 100){
            value = value.substring(0,100) +'...';
        }

      return value
    },
    colorfilter: function(value){
      var colorDict = {
        Punchng:"red",
        Premiumtime:"green",
        Vangaurd:"purple",
        Thenation: "cyan",
        TheNation: "cyan",
      };

      return colorDict.value
    }
  },
}
</script>

<style scoped>
p{
  font-size: 13px;
}

.news-card{
  /* border-radius: 10px; */
  box-shadow:1px 1px 3px 0px #eee;
  margin: 10px;
}
</style>