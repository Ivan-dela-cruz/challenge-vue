<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld 
      :user="user" 
      :exponente="exponente"
      :email="email"
      :password="password"
      :patients="patients"
      @auth-login="auth"
      @set-model="setValue"
      @get-patients="getPatients"
    />
  </div>
</template>

<script>
  import HelloWorld from './components/HelloWorld.vue'
  import axios from 'axios'

  function data() {
    return {
      exponente: 2,
      email: '',
      password: '',
      user:{
        name:null,
        lastName: null,
      },
      patients: [],
    }
  }

  function setValue({model, value}) {
    console.log(model, value);
    this[model] = value;
  }

  function auth() {
    const body  = {
      email: this.email,
      password: this.password
    };
    axios.post('https://hampi.cloud/api/login',body)
    .then((response) => { //success
      console.log(response);
      localStorage.setItem('token', response.data.token);
      localStorage.setItem('user', JSON.stringify(response.data.user));
      this.user = response.data.user;
      alert('success');
    })
    .catch((error) => { //error
      alert('error');
      console.log(error);
    });
  }

  function getPatients() {
    const token = localStorage.getItem('token');
    axios.get('https://hampi.cloud/api/patients',{
        headers: {
          'Authorization': `Bearer ${token}` 
        }
      }
    )
    .then((response) => { //success
      console.log(response);
      this.patients = response.data.patients;
    })
    .catch((error) => { //error
      alert('error');
      console.log(error);
    });
  }

  export default {
    name: 'App',
    components: {
      HelloWorld
    },
    data,
    methods:{
      auth,
      setValue,
      getPatients,
    }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
