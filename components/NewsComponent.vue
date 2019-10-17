<template>
  <a-card :bordered="false" style="width: 250px" class="news-card">
        <h3>{{ title }}}</h3>
        <p>{{ summary|truncate }}</p>
        <a :href="link"> Read More </a>
    </a-card>
</template>

<script>
export default {
    props: ['title', 'link', 'summary', 'date'],
    filters:{
        truncate: function(value){
        if(value.length > 100){
            value = value.substring(0,100) +'...';
        }

      return value
    }
  },
}
</script>

<style scoped>
p{
  font-size: 13px;
}

.news-card{
  border-radius: 10px;
  box-shadow:3px 4px 9px 7px #eee;
  margin: 10px;
}
</style>