<template>
  <div class="align-items-center">
      <h1>Project Todo-List</h1>
      <br>
          <div class="input-group">
                <input type="text" class="form-control" placeholder="ajouter votre ..." >
                <button class="btn btn-outline-secondary" type="button" >Ajouter</button>
                <button class="btn btn-outline-secondary" type="button">Annuler</button>
          </div>
          <br>
      <button class="btn btn-primary">Afficher</button>
      <br>
      <div>
        <table class="table ">
             <th>
                <td>Numero</td>
                <td>Todo list</td>
                <td>Action</td>
             </th>
             <tr>
                <td></td>
                <td></td>
                <td></td>
             </tr>
        </table>
      </div>
  </div>
</template>

<script>
export default {
  name: 'todo',
 
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-group{
  padding-left: 200px;
  padding-right: 200px;
}
table{
  text-align:center;
}

</style>
