<template>
  <div class="container">
    <div class="container-router">
      <router-link to="/">
        <span class="icon">
          <i class="fa-solid fa-arrow-right-from-bracket"></i>
        </span>
      </router-link> 
    </div>
    <div class="has-text-centered">
      <h1 class="title">Bienvenido</h1>
      <button class="button" @click="createEvent">Crear evento</button>

      <div class="event-card" v-show="show">
        <div class="field">
          <p class="control">
            <input class="input" type="text" name="name" v-model="name" placeholder="Nombre del evento">
          </p>
        </div>
        <input class="input" type="date" name="date" v-model="date">
        <input class="input" type="time" name="time" v-model="time">
        <button class="button" @click="saveEvent">Crear</button>
      </div>

    </div>

    <div class="container is-flex is-justify-content-center is-flex-wrap-wrap">

      <div class="card has-text-centered is-flex is-flex-direction-column is-justify-content-space-evenly">
        <h3 class="subtitle is-5 pt-3">Conferencia Vue.js</h3>
        <p> <b>Fecha:</b> 03/06/2022</p>
        <p> <b>Hora:</b> 5pm</p>
        <div>
          <button class="button fix mr-1">Asistir</button>
          <button class="button fix">Cancelar</button>
          <div class="has-text-centered">
            <button class="button remove">Eliminar evento</button>
          </div>
        </div>
      </div>

      <div class="card has-text-centered is-flex is-flex-direction-column is-justify-content-space-evenly" v-for="(e, id ) in events" :key="id">
        <h3 class="subtitle is-5 pt-3">{{e.name}}</h3>
        <p> <b>Fecha:</b> {{e.date}}</p>
        <p> <b>Hora:</b> {{e.time}}</p>
        <div>
          <button class="button fix mr-1">Asistir</button>
          <button class="button fix">Cancelar</button>
          <div class="has-text-centered">
            <button class="button remove" @click="remove(id)">Eliminar evento</button>
          </div>
        </div>
        <div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      show: false,
      events: [],
      name: "",
      date: "",
      time: "",
    }
  },
  mounted(){
    if(localStorage.getItem('events')){
      try{
        this.events = JSON.parse(localStorage.getItem('events'));
      }catch(e){
        localStorage.removeItem('events')
      }
    }
  },
  methods:{
    createEvent(){
      this.show = !this.show;
    },
    saveEvent(){
      let event = {date: this.date, name: this.name, time: this.time}
      this.events.push(event);

      this.date = "";
      this.name = "";
      this.time = "";

      this.save();
    },
    save(){
      const parsed = JSON.stringify(this.events);
      localStorage.setItem('events', parsed);
    },
    remove(id){
      this.events.splice(id,1);
      this.save();
    }
  }
}
</script>

<style scoped>
  .container{
    width: 100%;
    margin-top: 20px;
    padding: 10px;
  }
  .container-router{
    width: 100%;
    text-align: right;
  }
  i{
    color: var(--highlight);
    font-size: 25px;
  }
  h1{
    color: var(--blue-dark);
  }
  span{
    text-align: right;
  }
  .event-card{
    width: 200px;
    min-width: 190px;
    max-width: 300px;
    height: 250px;
    background-color: var(--white);
    border-radius: 15px;
    box-shadow: 0 4px 8px var(--blue);
    margin: 10px auto;
    padding: 25px 15px;
  }
  input{
    margin-bottom: 10px;
  }
  input::placeholder{
    font-size: 13px;
    color: #929aab;
  }
  .field:not(:last-child){
    margin-bottom: 0;
  }
  .card{
    width: 270px;
    min-width: 190px;
    max-width: 300px;
    height: 220px;
    background-color: var(--gray);
    border-radius: 15px;
    box-shadow: 0 4px 8px var(--blue);
    margin: 10px;
    padding-bottom: 10px;
  }
  h3{
    color: var(--highlight);
  }
  p{
    color: var(--text);
  }
  button{
    background-color: var(--white);
    border: 2px solid var(--blue);
    border-radius: 100px;
    font-family: 'Roboto', sans-serif;
    font-weight: 700;
    color: var(--highlight);
    margin-top: 5px;
  }
  button:hover{
    color: var(--white);
    background: var(--highlight);
    transition: background 1s;
  }
  .button:focus:not(:active){
    background: transparent;
    color: var(--blue-light);
    box-shadow: none;
    border: 2px solid var(--highlight);
  }
  .fix{
    width: 90px;
    font-size: 12px;
  }
  .remove{
    width: 80px;
    font-size: 10px;
    border: 1px solid #c82121;
    color: var(--blue);
  }
  .remove:hover{
    background: #929aab;
  }
  .remove:focus:not(:active){
    background: transparent;
    color: #c82121;
    box-shadow: none;
    border: 2px solid #929aab;
  }
</style>
