<script>
var db;
    let openRequest = indexedDB.open("idbdwec", 1);

    openRequest.onupgradeneeded = function() {
        // se dispara si el cliente no tiene la base de datos
        let db = openRequest.result;
        switch (event.oldVersion) { // versión de db existente
            case 0:
                // version 0 significa que el cliente no tiene base de datos
                // ejecutar inicialización
                let db = openRequest.result;
                if (!db.objectStoreNames.contains('usuarios')) { // si no hay un almacén de usuarios 

                    const store = db.createObjectStore('usuarios', {
                        keyPath: 'id',
                    });

                    store.createIndex('mail', 'mail', {
                        unique: false
                    });

                    store.createIndex('password', 'password', {
                        unique: false
                    });

                    store.createIndex('log', 'log', {
                        unique: false
                    });


                    console.info("creamos usuarios!")
                } else {
                    console.info("tenemos usuarios!")
                }
            case 1:
                // el cliente tiene la versión 1
                // actualizar
                //let deleteRequest = indexedDB.deleteDatabase(name)
                //db.deleteObjectStore('usuarios')

        }
    };

    openRequest.onerror = function() {
        console.error("Error", openRequest.error);
    };

    openRequest.onsuccess = function() {
        db = openRequest.result;
        // continúa trabajando con la base de datos usando el objeto db
        console.info("tenemos bd!")
    };

export default {
  data: () => ({
    mail: "",
    password: "",
    firstName: "",
    lastName: "",
    telephone: "",
    firstNameRules: [
      (value) => {
        if (value?.length > 2 && /[^0-9]/.test(value)) return true;

        return "El nombre debe tener por lo menos 3 letras y no pueden ser digitios.";
      },
    ],
    lastNameRules: [
      (value) => {
        if (value?.length > 2 && /[^0-9]/.test(value)) return true;

        return "El apellido debe tener por lo menos 3 letras y no pueden ser digitios.";
      },
    ],
    telephoneRules: [
      (value) => {
        if (value?.length == 9 && /[0-9]/.test(value)) return true;

        return "El numero de telefono solo debe tener numeros y debe tener una longitu de 9 digitos.";
      },
    ],
    mailRules: [
      (value) => {
        if (/\S+@\S+\.\S+/.test(value)) return true;

        return "El correo no es correcto.";
      },
    ],
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
    insertarIndexed() {
      var id = 1;
      var mail = this.mail;
      var password = this.password;

        let transaction = db.transaction("usuarios", "readwrite"); // (1)
        console.log("conectado");
        // obtiene un almacén de objetos para operar con él
        let usuarios = transaction.objectStore("usuarios"); // (2)
        console.log("lista creada");
        let usuario = {
          id: id,
          mail: mail,
          password: password,
        }
        console.log("usuario creado");
        let request = usuarios.add(usuario); // (3)
        console.log("usuario en listado");
        request.onsuccess = function () {
          // (4)
          console.log("Usuario agregado", request.result);
        };

        request.onerror = function () {
          console.log("Hay un error", request.error);
        };
     
    },
  },
};
</script>

<template>
  <div class="m-5">
    <v-sheet width="300" class="mx-auto">
      <h1 class="text-center">Regiser From</h1>
      <br />
      <v-form fast-fail @submit.prevent>
        <v-text-field
          v-model="firstName"
          label="Nombre"
          :rules="firstNameRules"
        ></v-text-field>

        <v-text-field
          v-model="lastName"
          label="Apellido"
          :rules="lastNameRules"
        ></v-text-field>

        <v-text-field
          v-model="mail"
          label="Correo"
          :rules="mailRules"
        ></v-text-field>

        <v-text-field
          v-model="telephone"
          label="Numero de telefono"
          :rules="telephoneRules"
        ></v-text-field>

        <v-text-field
          v-model="password"
          label="Contraseña"
          :rules="passwordRules"
        ></v-text-field>

        <v-btn type="submit" block class="mt-2" @click="insertarIndexed"
          >Submit</v-btn
        >
      </v-form>
    </v-sheet>
  </div>
</template>
