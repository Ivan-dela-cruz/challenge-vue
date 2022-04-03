<template>
  <div class="hello">
    <h1>Bienvenido {{user.name}}</h1>
    <input placeholder="email" type="text" @input="setModel('email',$event.target.value)">
    <input placeholder="password" type="text" @change="increment" @input="setModel('password',$event.target.value)">
    <button @click="authLogin"> Login</button>
    <button @click="$emit('get-patients')"> Obtener pacientes</button>

    <ul>
      <li v-for="p in patients" :key="p.id">
        <span> {{p.name}} {{p.last_name}} </span>
      </li>
    </ul>
  </div>
</template>

<script>
  function created() {
    console.log('created');
  }

  function mounted() {
    console.log('mounted');
  }

  function increment() {
    this.count = this.count * this.exponente;
  }

  function dism() {
    this.count --;
  }

  function authLogin() {
    this.$emit('auth-login')
  }

  function setModel(model, value) {
    this.$emit('set-model', {model, value})
  }

  function data() {
    return {
      title: '',
      count: 1,
      isActivate: false,
    }
  }

  export default {
    name: 'HelloWorld',
    props: {
      user: Object,
      exponente: Number,
      email: String,
      password: String,
      patients: Array,
    },
    data,
    created,
    mounted,
    methods: {
      increment,
      dism,
      authLogin,
      setModel,
    }
  }
</script>

<style scoped>
  h3 {
    margin: 40px 0 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  a {
    color: #42b983;
  }
</style>
