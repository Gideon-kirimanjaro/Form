<template>
  <v-app>
    

    <v-main>
      <form-container></form-container>
    </v-main>
  </v-app>
</template>

<script>
import Form from './components/Form/Form'

export default {
  name: 'App',
  data(){
    return{
      name: 'Gideon'
    }
  },

  components: {
    'form-container': Form,
    
  },

  beforeCreate(){
    alert('before Create')
  },
  created(){
    alert('Created')
  },
  beforeMount(){
    alert('Before Mounted')
  },
  mounted(){
    alert('Mounted')
  },
  beforeUpdate(){
    alert('Before Update')
  },
  updated(){
    alert('Updated')
  }

};
</script>
