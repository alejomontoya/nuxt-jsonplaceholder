<template>
  <div class="container mt-5">
      <div class="card">
        <div class="card-body">
          <h3>{{articulo.title}}</h3>
          <p class="small">{{articulo.autor}}</p>
          <p>{{articulo.body}}</p>
          <nuxt-link to="/blog" class="btn btn-primary">Atras</nuxt-link>
        </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data(){
    return {
    
    }
  },
  // async created(){
    
  // },
  async asyncData({isDev,route,store,env,params,query,req,res,redirect,error}){
    try {
      const res = await axios.get(`https://jsonplaceholder.typicode.com/posts/${params.id}`);
     
      const articulo = res.data;

      const resAutor = await axios.get(`https://jsonplaceholder.typicode.com/users/${res.data.userId}`);
      
      articulo.autor = resAutor.data.name;
      
      return {articulo};
      
    } catch (error) {
      // console.log(error);

      return {error: error}
    }
  }
}
</script>

<style>

</style>