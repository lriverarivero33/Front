<template>
  <v-app>
  <v-main >
    <v-row>
      <v-col
        class="text-center"
        cols="16">
        
      <v-alert
      
      v-if= "error"
      prominent
      :type= "typeError"
      width="500" 
      class="mx-auto mt-1"
      
    >
      <v-row align ="center"  @click:append= "error = ! error" >
        <v-col class="grow">
          {{error_msg}}
        </v-col>
        <v-col class="shrink">
          <v-btn  @click = "error = ! error, usuario='', password=''">Reintentar!</v-btn>
        </v-col>
      </v-row>
    </v-alert>
    <br>
            <br>
            <br>
            <br>
            <br>
            <br>
        <div id="card">
          <v-card   width="600" height="800" class="mx-auto mt-auto" elevation="24">
            <br>
            <br>
            <br>
            <br>
            <br>
            <v-img src="../assets/bienvenido.png"></v-img>
      
            <v-card-title  > Inicia Sesion </v-card-title>
      <v-card-text >
        <form v-on:submit.prevent="login">
        <br>
        <br>
        <br>
          <v-text-field 
          label="Username" 
          prepend-icon="mdi-account-circle" 
          v-model="usuario"/>


        <v-text-field 
          label="Password" 
          :type= "MostrarContraseña ? 'text' : 'Password'" 
          prepend-icon="mdi-lock" 
          :append-icon="MostrarContraseña ? 'mdi-eye' : 'mdi-eye-off'"
          @click:append="MostrarContraseña = ! MostrarContraseña"
          v-model= "password"
        />
        <div>
        <v-btn color="success" type="submit" value="login">Login</v-btn>
        <v-col></v-col>
        <v-btn color="info" left= "true" >Register</v-btn>
      </div>
      </form>
      </v-card-text>
    </v-card>
    </div>
  <p></p>
      <v-col cols="6">
          </v-col>
      </v-col>

    </v-row>
  </v-main>
</v-app>

</template>


<script>
import axios from 'axios'
export default {
  name: 'App',

   data () {
    return  {
      MostrarContraseña: false,
      usuario: "",
      password: "",
      error: false,
      error_msg:"",
      typeError:"",
  }},
  methods:{
    login(){
           let json = {
        "nickname" : this.usuario,
        "password" : this.password
      };
      

      axios.post('https://marcosrepositorio.herokuapp.com/auth', json)
      .then( response =>{
         console.log(response.data)
        if(response.status == 500){
            console.log("error conexion")
             //localStorage._id = data.data.result._id;
             //this.$router.push('dashboard');
        }
          else{ 
            if(response.data == "No digito ningun campo"){
            this.error = true;
              this.error_msg = "Por favor digite los campos";
              this.typeError = "info";
          } 
          else if(response.data == "No ingreso Usuario"){
              this.error = true;
              this.error_msg = "Por favor ingrese un Usuario";
              this.typeError = "error";
          }
          else if(response.data == "No ingreso contraseña"){
            this.error = true;
            this.error_msg = "Por favor ingrese una contraseña";
            this.typeError = "error";
          }
          else if( response.data == "Usuario invalido" || response.data == "No existe el usuario"){
              this.error = true;
              this.error_msg = "Usuario o contraseña invalido";
              this.typeError = "warning";
            }
            else{
              this.error = true;
              this.error_msg = "Success";
              this.typeError = "success";
              console.log(response.data, "Todo correcto");
          this.$router.push('about');
            }
          }
      })
    }

  },
  mounted() {
   /* this.axios.get('https://marcosrepositorio.herokuapp.com/peoples')
    .then((response) => {
       console.log(response.data)
        this.items = response.data;
      })*/
  },


};
</script>
<style scoped>
   .maregenes{
    margin-top:-6.2%;
    margin-bottom: 4%;
    width: 400px;
    height: 100px;
    
   

  }
  main{
    background:url("../assets/fondo.jpg");

    background-size: cover;
  }
  .mx-auto {
  margin: 20px;
  box-shadow: 9px 9px 9px rgba(128,128,128,0.6);
}
.mx-auto:hover {
  box-shadow: 9px 9px 9px rgba(20,20,20,0.6);
}
  </style>