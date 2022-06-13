<template>
  <div class="container">
    <form v-on:submit="submitHandler" class="formulario">
      <div class="welcome_text_container">
        <div class="text_container">
          <h1>Frente</h1>
          <h1>Republicano</h1>
          <h1>Tandil</h1>
        </div>
        <h2>Votá por tu horario ideal!</h2>
      </div>
      <div class="input_container">
        <!-- <input required class="input" v-model="nombre" placeholder="Nombre" /> -->
        <!-- <input required class="input" v-model="apellido" placeholder="Apellido" /> -->
        <!-- <input required class="input" type="number" v-model="telefono" placeholder="Teléfono" /> -->
        <!-- <input required class="input" type="email" v-model="email" placeholder="E-mail" /> -->
        <!-- <input required class="input" v-model="localidad" placeholder="Localidad" /> -->

        <select name="" id="" v-model="horario">
          <option value="" selected disabled>Selecciona tu horario ideal</option>
          <option value="lunes19">Lunes 19hs</option>
          <option value="lunes20">Lunes 20hs</option>
          <option value="martes19">Martes 19hs</option>
          <option value="martes20">Martes 20hs</option>
          <option value="miercoles19">Miércoles 19hs</option>
          <option value="miercoles20">Miércoles 20hs</option>
          <option value="jueves19">Jueves 19hs</option>
          <option value="jueves20">Jueves 20hs</option>
          <option value="viernes19">Viernes 19hs</option>
          <option value="viernes20">Viernes 20hs</option>
          <option value="sabadom">Sábado de mañana</option>
          <option value="sabadot">Sábado de tarde</option>
        </select>
      </div>
      <Button :type="'submit'">Guardar</Button>
    </form>

    <Transition>
      <Popup v-if="success || error" :class="{ error: error, success: success }" :message="message" />
    </Transition>
  </div>
</template>

<script>
import Button from '../components/UI/Button.vue';
import Popup from '../components/UI/Popup.vue';


export default {
  name: 'IndexPage',
  components: {
    Button,
    Popup,
  },
  data: () => ({
    horario: "",
    // nombre: '',
    // apellido: '',
    // telefono: '',
    // email: '',
    // localidad: '',
    success: false,
    error: false,
    message: ""
  }),
  methods: {
    submitHandler(e) {
      e.preventDefault();

      // let payload = {
      //   nombre: this.nombre,
      //   apellido: this.apellido,
      //   telefono: this.telefono,
      //   email: this.email,
      //   localidad: this.localidad,
      // }

      let payload = {
        horario: this.horario,
      }

      console.log(payload);
      if (!this.empty(payload)) {
        // this.setEmpty();

        this.success = true;
        this.message = "Toda la info se envió correctamente.";
        setTimeout(() => {
          this.success = false;
        }, 5000);


        fetch("https://cefcepromoapi.000webhostapp.com/api/horario",
          {
            headers: {
              // 'Accept': 'application/json',
              // 'Content-Type': 'application/json'
            },
            method: "POST",
            body: JSON.stringify(payload)
          })
          .then(function (res) { console.log(res) })
          .catch(function (res) { console.log(res) })
      } else {
        this.error = true;
        this.message = "Por favor checkee todos los campos.";
        setTimeout(() => {
          this.error = false;
        }, 1500);
      }
    },

    empty(payload) {
      if (payload.horario == null || payload.horario == '') {
        return true;
      }
      // else if (payload.apellido == null || payload.apellido == '') {
      //   return true;
      // }
      // else if (payload.telefono == null || payload.telefono == '') {
      //   return true;
      // }
      // else if (payload.email == null || payload.email == '') {
      //   return true;
      // }
      // else if (payload.localidad == null || payload.localidad == '') {
      //   return true;
      // }
      return false;
    },
    // setEmpty() {
    //   this.nombre = '';
    //   this.apellido = '';
    //   this.telefono = '';
    //   this.email = '';
    //   this.localidad = '';
    // }
  }

}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}


html,
body {
  height: 100vh;
  background-color: #d4d8e4;
}

.container {
  width: 100%;
  height: 100vh;
  /* height: 100%; */
  /* background-color: red; */
  display: flex;
  background-color: #6e4d9c;
  justify-content: center;
  align-items: center;
}

.welcome_text_container {
  margin: 15% 0;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.welcome_text_container h2 {
  margin-top: 5%;
  font-weight: 300;
}

.text_container {
  width: 80%;
  /* height: 50%;   */
  border: 3px solid #6e4d9c;
  padding: -20% 20%;
}


.text_container h1 {
  padding-left: 7.5%;
  color: #6e4d9c;
  font-size: 2.5rem;
  font-weight: 700;
}

.highlight {
  font-weight: 500;
  color: #6e4d9c;
}

.formulario {
  margin-top: 7.5%;
  width: 90%;
  height: 90%;
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 10px;
}

.formulario .input_container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.formulario>div.input_container * {
  margin: 10% 0;
}

.formulario button {
  margin: 10% 0;
}

.input {
  display: block;
  border: none;
  border-bottom: 1px solid gray;
  width: 90%;
  font-weight: 300;
  font-size: 1.5rem;
  background-color: transparent;

}

.input:focus {
  outline: none ! important;
}



.v-enter-active,
.v-leave-active {
  transition: opacity 5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>