<template>
  <div class="app-container app-theme-white">

    <transition name="fade" mode="out-in" appear>
            <Header />
        </transition> 
 <!-- <toolbar></toolbar> -->
  <transition name="fade" mode="out-in" appear>
            <Sidebar />
        </transition>
 <!--  <navigation></navigation> -->
  
         <v-content>
         
           <router-view/>
         
         </v-content>
  </div>

   
</template>

<script>
 /*import toolbar from '../components/core/Toolbar'*/
 /*import navigation from '../components/core/NavigationDrawer'
  */
  import Header from "../components/core/Header";
 import Sidebar from '../components/core/Sidebar'
 
  export default {
    components:{
      /* toolbar : toolbar,*/
      /*navigation : navigation*/
      Sidebar,
      Header
    },


    data() {
    return {
     
      }
    }
  
    
  }
</script>

