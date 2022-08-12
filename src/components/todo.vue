<template>
  <div class="align-items-center">
      <h1>Project Todo-List</h1>
      <br>
          <div class="input-group">
                <input type="text" class="form-control" placeholder="ajouter votre ..." v-model="todo" >
                <button class="btn btn-outline-secondary b1" type="button" @click="ajouter" >Ajouter</button>
                <button class="btn btn-outline-secondary b1" type="button" @click="annuler">Annuler</button>
          </div>
          <br>
      <button class="btn  b2 " @click="afficher">Afficher</button>
      <br>
      <br>
     <table class="table">
  <thead>
    <tr> 
      <th scope="col">Numero</th>
      <th scope="col">Todo</th>
      <th scope="col">Status</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="post in posts">
      
      <td>{{post.id}}</td>
      <td>{{post.todo}}</td>
      <td>{{post.status}}</td>
      <td><button @click="supprimer(post.id)" class="btn btn-danger btn-sm">delete</button>&nbsp
      <button  class="btn btn-info btn-sm" @click.once="finished(post.id)">Finished</button>
      </td>
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
      todo:'',
      sup:true
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
      if(this.todo==''){
        alert("remplir le champ")
      }
      else{
        this.i=this.i+1
         let result = await axios.post("http://localhost:3000/posts",{
                      numero:this.i,
                      todo:this.todo,
                      status:'in progress'
                  })
                  console.warn(result)
                  if(result.status==201){
                          alert("vous voulez vraiment ajouter ")
                  }
        this.afficher()
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
       this.afficher()

    },
    async finished(id){
      let result=await axios.put(`http://localhost:3000/posts/${id}`,{
        todo:this.todo,
        status:'completed'
      }).then(response=>{
        console.log(response)
      })
      this.afficher()
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
.table{
  color:#fff;
}
.b1{
  background-color: #256D85;
  color:#fff;
}
.b2{
  background-color: #256D85;
  color: #fff;
}
.b2:focus{
  background-color: aqua;
}


</style>
