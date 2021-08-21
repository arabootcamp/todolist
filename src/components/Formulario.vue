<template>
  <div class="container my-5 text-center">
    <h1 class="text-secondary">Crear una nueva tarea</h1>
    <form class="mt-4" action="">
      <label class="form-label" for="text">Tarea</label>
      <div class="form-group row">
        <div class="col-xs-13 col-md-5 
        mx-auto">
          <input v-model="input" class="form-control" type="text" name="text" id="text"
            placeholder="ingresa una nueva tarea" maxlength="40"
            title="Debe tener al menos 1 carácter y comenzar con letra o número." autocomplete="off">
        </div>
      </div>
      <p class="my-5 fs-4 text-danger"><span class="invisible">_</span>{{input}}</p>
      <div>
        <button @click="insertItem($event)" class="btn btn-success">Insertar</button>
        <button v-on:click="sortItems($event)" class="btn btn-warning mx-2">Ordenar</button>
        <button v-on:click="deleteItem($event)" class="btn btn-danger">Eliminar</button>
      </div>
    </form>
    <div class="d-inline-block text-center my-5">
      <h2 class="text-secondary">Lista</h2>
      <ul class="">
        <li class="text-start" v-for="(item,index) in array" :key="index">{{item}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Formulario',
    data() {
      return {
        input: '',
        array: []
      }
    },
    methods: {
      validarInput: (element) => {
        let empty = 0;
        let max = element.length;
        for (let i; i < max; i++) {
          if (element[i] == ' ')
            empty++;
          else
            break;
        }
        if (element.length == 0 || element[0] == ' ' || element[max - 1] == ' ' || (empty == max)) {
          alert("Debe ingresar una palabra que comience y termine con un carácter distinto a vacio.");
          return false;
        } else
          return true;
      },
      noExistItem: (element, array) => {
        let response = array.find(data => data.toUpperCase() == element.toUpperCase());
        if (response == null)
          return true;
        else {
          alert('Ya esta en la lista: ' + element + '\n\n(ejemplo: uno, Uno, UNO se consideran 3 palabras iguales)');
          return false;
        }
      },
      insertItem: function (event) {
        event.preventDefault(); //con esta intruccion detengo la comprobación del minlenght, requerid ....
        if (this.validarInput(this.input) && this.noExistItem(this.input, this.array)) {
          this.array.push(this.input.toLowerCase());
          this.input = '';
        }
      },
      sortItems: function (event) {
        event.preventDefault();
        this.array.sort();
      },
      deleteItem: function (event) {
        event.preventDefault();
        let out = this.input.toLowerCase();
        if (this.validarInput(out)) {
          let indexof = this.array.indexOf(out);
          if (indexof == -1)
            alert('Palabra no esta en la lista');
          else {
            this.array.splice(indexof, 1);
            this.input = '';
          }
        }
      }
    }
  }
</script>