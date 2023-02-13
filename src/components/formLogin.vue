<script>
var db;
let openRequest = indexedDB.open("idbdwec", 1);

openRequest.onupgradeneeded = function () {
  // se dispara si el cliente no tiene la base de datos
  let db = openRequest.result;
  switch (
    event.oldVersion // versión de db existente
  ) {
    case 0:
      // version 0 significa que el cliente no tiene base de datos
      // ejecutar inicialización
      let db = openRequest.result;
      if (!db.objectStoreNames.contains("usuarios")) {
        // si no hay un almacén de usuarios

        const store = db.createObjectStore("usuarios", {
          keyPath: "id",
        });

        store.createIndex("mail", "mail", {
          unique: false,
        });

        store.createIndex("password", "password", {
          unique: false,
        });

        console.info("creamos usuarios!");
      } else {
        console.info("tenemos usuarios!");
      }
    case 1:
    // el cliente tiene la versión 1
    // actualizar
    //let deleteRequest = indexedDB.deleteDatabase(name)
    //db.deleteObjectStore('usuarios')
  }
};

openRequest.onerror = function () {
  console.error("Error", openRequest.error);
};

openRequest.onsuccess = function () {
  db = openRequest.result;
  // continúa trabajando con la base de datos usando el objeto db
  console.info("tenemos bd!");
};

export default {
  data: () => ({
    log: true,
    mail: "",
    mailRules: [
      (value) => {
        if (/\S+@\S+\.\S+/.test(value)) return true;

        return "El correo no es correcto.";
      },
    ],
    password: "",
    passwordRules: [
      (value) => {
        if (
          /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[$@$!%*?&])[A-Za-z\d$@$!%*?&]{8,15}$/.test(
            value
          )
        )
          return true;

        return "La contraseña debe tener minimo 8 caracteres, maximo 15 caracteres, al menos una letra mayúscula, al menos una letra minucula, al menos un dígito ,no debe tener espacios en blanco y al menos 1 caracter especial.";
      },
    ],
  }),
  methods: {
    loguearse() {
      let mail = this.mail;
      let password = this.password;
      var objectStore = db.transaction("usuarios").objectStore("usuarios");
      objectStore.openCursor().onsuccess = function (event) {
        var cursor = event.target.result;
        if (cursor) {
          if (cursor.value.mail == mail && cursor.value.password == password) {
            console.log("Estas logueado");
          }
          console.log(cursor.value.mail);
          console.log(cursor.value.password);
          cursor.continue();
        } else {
          console.log("¡No hay más registros disponibles!");
        }
      };
    },
   
  },
};
</script>

<template>
  <div class="m-5">
    <v-sheet width="300" class="mx-auto">
      <h1 class="text-center">Login From</h1>
      <br />
      <v-form fast-fail @submit.prevent>
        <v-text-field
          v-model="mail"
          label="Correo"
          :rules="mailRules"
        ></v-text-field>

        <v-text-field
          v-model="password"
          label="Contraseña"
          :rules="passwordRules"
        ></v-text-field>

        <v-btn type="submit" block class="mt-2" @click="loguearse"
          >Submit</v-btn
        >
      </v-form>
    </v-sheet>
  </div>
</template>
