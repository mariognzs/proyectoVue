<script>
export default {
  data: () => ({
    product: {
      name: "",
      description: "",
    },
    products: {
      names: [],
      descriptions: [],
    },

    nameRules: [
      (value) => {
        if (value?.length > 2 && /[^0-9]/.test(value)) return true;

        return "El nombre debe tener por lo menos 3 letras y no pueden ser digitios.";
      },
    ],
    descriptionRules: [
      (value) => {
        if (value?.length > 2 && /[^0-9]/.test(value)) return true;

        return "El apellido debe tener por lo menos 3 letras y no pueden ser digitios.";
      },
    ],
  }),
  methods: {
    guardar: function () {
      this.products.names.push(this.product.name);
      this.products.descriptions.push(this.product.description);
    },
    eliminar: function (i) {
      let pos = i;
      this.products.names.splice(pos, 1);
      this.products.descriptions.splice(pos, 1);
    },
    modificar: function (i) {
      let pos = i;
      this.products.names[pos] = this.product.name;
      this.products.descriptions[pos] = this.product.description;
    },
  },
};
</script>

<template>
  <div class="m-5">
    <h1 class="text-center">Regiser Product From</h1>
    <br />
    <v-sheet width="300" class="mx-auto">
      <v-form fast-fail @submit.prevent>
        <v-text-field
          v-model="product.name"
          label="Nombre"
          :rules="nameRules"
          required
        ></v-text-field>

        <v-text-field
          v-model="product.description"
          label="Descripcion"
          :rules="descriptionRules"
          required
        ></v-text-field>

        <v-btn type="submit" block class="btn mt-2 btn-success" @click="guardar"
          >Guardar</v-btn
        >
      </v-form>
    </v-sheet>
  </div>

  <!-- CRUD -->
  <v-table class="m-5">
    <thead>
      <tr>
        <th class="text-center">#</th>
        <th class="text-center">Nombre</th>
        <th class="text-center">Descripción</th>
        <th class="text-center">Modificar</th>
        <th class="text-center">Eliminar</th>
      </tr>
    </thead>
    <tbody>
      <tr class="text-center" v-for="(name, i) in products.names" :key="i">
        <td>{{ i + 1 }}</td>
        <td>{{ name }}</td>
        <td>{{ products.descriptions[i] }}</td>
        <td>
          <button
            :idButton="i"
            type="button"
            class="btn btn-outline-warning"
            @click="modificar(i)"
          >
            Modificar
          </button>
        </td>
        <td>
          <button
            type="button"
            class="btn btn-outline-danger"
            @click="eliminar(i)"
          >
            Eliminar
          </button>
        </td>
      </tr>
    </tbody>
  </v-table>
</template>
