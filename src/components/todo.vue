<template>
  <div class="align-items-center">
      <h1>Project Todo-List</h1>
      <br>
          <div class="input-group">
                <input type="text" class="form-control" placeholder="ajouter votre ..." v-model="todo" >
                <button class="btn btn-outline-secondary" type="button" @click="ajouter" >Ajouter</button>
                <button class="btn btn-outline-secondary" type="button" @click="annuler">Annuler</button>
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
      
      <td>{{post.id}}</td>
      <td>{{post.todo}}</td>
      <td><button @click="supprimer(post.id)">supprimer</button><button>Modifier</button></td>
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
      i:0,
      todo:''
    }
        
  },
 methods:{
  async afficher(){
   await axios.get("http://localhost:3000/posts")
            .then(result => {
              this.posts = result.data;
              })
              console.table(this.posts)
    },
 /*   async ajouter(){
      this.i=this.i+1
      let result=await axios.post("http://localhost:3000/posts",{
        numero:this.i,
        todo:this.todo
      }).then(res=>{
        console.log(result.status)
      })
    }*/
    async ajouter(){
      this.i=this.i+1
       let result = await axios.post("http://localhost:3000/posts",{
                    numero:this.i,
                    todo:this.todo
                })
                console.warn(result)
                if(result.status==201){
                        alert("sign up")
                }
    },
    annuler(){
      this.todo=''
    },
    async supprimer(id){
      let result=await axios.delete(`http://localhost:3000/posts/${id}`)
      .then(response=>{
        console.log(response)
      })

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
