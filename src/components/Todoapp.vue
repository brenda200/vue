<template>
 <div class="container" style="max-width: 600px">
    
    <h2 class="text-center mt-5">Rillsoft</h2>

   
    <div class="d-flex mt-5">
      <input
        type="text"
        v-model="camponome"
        placeholder="Nome"
        class="w-100 form-control"
      />

 <input
        type="text"
        v-model="Telefone"
        placeholder="Telefone"
        class="w-100 form-control"
      />

      <button class="btn btn-warning rounded-0" @click="submitNome">
        ENVIAR
      </button>
    </div>
    
    
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Nome</th>
          <th scope="col" style="width: 120px">Telefone</th>
          <th scope="col" style="width: 120px">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in Nome" :key="index">
          <td>
            <span :class="{ 'line-through': item.status === 'finished' }">
              {{ item.Nome }}
            </span>
          </td>
          <td>
            <span :class="{ 'line-through': item.status === 'finished' }">
              {{ item.Telefone }}
            </span>
          </td>
          <td>
            <span
              class="pointer noselect"
              @click="changeStatus(index)"
              :class="{
                'text-danger': item.status === 'to-do',
                'text-success': item.status === 'finished',
                'text-warning': item.status === 'in-progress',
              }"
            >
              {{ capitalizeFirstChar(item.status) }}
            </span>
          </td>
          <td class="text-center">
            <div @click="deleteNome(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          <td class="text-center">
            <div @click="editTelefone(index)">
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'App',
  props: {
  msg: String,
  },

  data(){
    return {
      camponome: "",
      editedNome: null,
      statuses: ["to-do", "in-progress", "finished"],

      Nome: [
        {
          Nome: "Steal bananas from the supermarket.",
          status: "to-do",
      
        },
        {
          Nome: "Eat 1 kg chocolate in 1 hour.",
          status: "in-progress",
        },
        {
          Nome: "Create YouTube video.",
          status: "finished",
        },
      ],
    };
  },


methods: {
   capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.Nome[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.Nome[index].status = this.statuses[newIndex];
    },
     deleteNome(index) {
      this.Nome.splice(index, 1);
    },

     editNome(index) {
      this.Nome = this.Nome[index].Nome;
      this.editedNome = index;
    },
    submitNome(){
      if (this.Nome.length === 0)return;

      if (this.editedNome !=null){
        this.tasks[this.editNome]
      
      }

      this.Nome.push({
          Nome: this.camponome,
          Telefone: this.Telefone,
          status: "todo",
      });

    }
}
}

</script>

<style scoped>
.pointer{
  cursor: pointer;
}
.noselect {
  -webkit-touch-callout: Nome;
 -webkit-user-select: None;
 -khtml-user-select: None;
 -moz-user-select: Nome;
 -ms-user-select: Nome;
 user-select: Nome;

}

.line-through {
  text-decoration: line-through;
}
</style>>





