<template>
  <div class="align-items-center">
      <h1>Project Todo-List</h1>
      <br>
          <div class="input-group">
                <input type="text" class="form-control" placeholder="ajouter votre ..." >
                <button class="btn btn-outline-secondary" type="button" @click="ajouter" >Ajouter</button>
                <button class="btn btn-outline-secondary" type="button">Annuler</button>
          </div>
          <br>
      <button class="btn btn-primary" @click="afficher">Afficher</button>
      <br>
      <br>
     <table class="table">
  <thead>
    <tr>
      
      <th scope="col">Numero</th>
      <th scope="col">Todo</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="post in posts">
      
      <td>{{post.numero}}</td>
      <td>{{post.todo}}</td>
      <td><button>supprimer</button><button>Modifier</button></td>
    </tr>
  </tbody>
</table>
     
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'todo',
  data(){
    return{
      posts:null,
      i:0
    }
        
  },
 methods:{
  //async ajouter(){
           // Création d'une promesse qui va contenir l'appel
    //       const response = await axios.get('http://localhost:3000/posts')
            // Avec la méthode "then", on extrait les données
      //    this.todo=response.data
        //  console.log(response.data)
  //}
  async afficher(){
   await axios.get("http://localhost:3000/posts")
            .then(result => {
              this.posts = result.data;
              })
              console.table(this.posts)
    }
 }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-group{
  padding-left: 200px;
  padding-right: 200px;
}


</style>
