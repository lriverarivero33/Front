   <template >
      <v-app id="inspire">
        <div class="app-container">
        
         
                 <v-content>
            <router-view/>
          
          </v-content>
        </div>
      </v-app>
    </template>

<script>

  export default {
    name: 'App',
    
    data() {
      return {
        drawer: true
      }
    }
  }
  </script>
  
  <style lang="scss">
    @import "assets/base.scss";
  </style>