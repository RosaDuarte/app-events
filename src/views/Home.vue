<template>
  <div class="container-main">
    <div class="pt-5">
      <h2 class="title has-text-centered">Eventos</h2>
      <p class="has-text-centered m-4">Si quieres participar en nuestros eventos solo debes registrarte e ingresar ¡Te esperamos!</p>
    </div>
    <div class="home is-flex is-flex-direction-column is-justify-content-center is-align-items-center pt-4 pb-4" id="home">
      <entry />
      <register />
    </div>
  </div>
</template>

<script>
import Entry from '@/components/Entry'
import Register from '@/components/Register'

export default{
  name: "Home",
  components: {Entry, Register}
  }
</script>

<style scoped>
  h2{
    color: var(--blue-dark);
  }
  p{
    color: var(--highlight);
    font-weight: 700;
  }
  .home{
    width: 100%;
  }

  @media (min-width: 769px) {
    .container-main{
      padding-top: 20px;
    }
    #home{
      flex-direction: row-reverse!important;
    }
    h2{
      font-size: 45px;
    }
    p{
      font-size: 25px;
    }
    .box:not(:last-child){
      margin: 40px 20px;
    }
  }
</style>

