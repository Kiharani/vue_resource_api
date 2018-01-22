<template>
  <div class="sourceselection">
    <div class="jumbotron mx-auto">
      <p class="h2"><i class="fa fa-list-alt"></i> News List: Latest News from accross the Globe</p>
      <p class="h4">Select News source</p>
      <select class="form-control" v-on:change="sourceChanged">
        <option value="">Select News Source</option>
        <option v-bind:value="source.id" v-for="source in sources">{{source.name}}</option>
      </select>
      <div v-if="source">
        <p class="my-3">{{source.description}}</p>
        <a v-bind:href="source.url" class="btn btn-outline-primary" target="_blank">Visit {{source.name}} Website</a>
      </div>
    </div>
  </div>
</template>

<script>
  export default{
    name:'sourceselection',
    data(){
      return{
        sources:[],
        source:''
      }
    },
    methods:{
      sourceChanged: function(e){
        for(var i = 0; i < this.sources.length; i++){
          if(this.sources[i].id == e.target.value){
            this.source = this.sources[i];
          }
        }
        this.$emit('sourceChanged', e.target.value);
      }
    },
    created: function(){
      this.$http.get('https://newsapi.org/v1/sources?language=en')
      .then(response => {
        this.sources = response.data.sources;
      });
    }
  }
</script>

<style scoped>

</style>
