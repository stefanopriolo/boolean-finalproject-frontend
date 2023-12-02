<script>
import Presentation from "./components/Presentation.vue";

export default {
  components: {
    Presentation,
  },

  data() {
    return {};
  },
  methods: {},

  mounted() {},
};
</script>

<template>
  <header>
    <div class="navigation-menu">
      <!-- colonna col-4 con bg-scuro -->
      <div class="row logo-column">
        <div class=" ">
          <img src="/logocyber.png" class="logo ms-3" alt="Logo" />
        </div>
      </div>

      <div class="menu-items">
        <router-link class="me-5" to="/">Home</router-link>
        <a class="me-3" href="http://127.0.0.1:8000/login">Login</a>
        <a class="me-3" href="http://127.0.0.1:8000/register">Register</a>
      </div>
    </div>
  </header>

  <main>
    <router-view></router-view>
  </main>

  <footer></footer>
</template>

<style lang="scss">

::-webkit-scrollbar{
    background: #1e3240ea;
}
::-webkit-scrollbar-thumb{
    border-radius: 100px;
}
::-webkit-scrollbar-thumb:hover{
    background-color:  #27cdf23b;
}

header{
  background-color: #27cdf21f;
    box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.1);
    /* border-bottom: 1px solid black; */
    width: 100%;
    position: fixed;
}



.navigation-menu {
  display: flex;
}

.logo-column {
  width: 33.73%;
  padding: 1rem;
}

.logo {
  width: 2.2rem;
}

.menu-items {
  flex-grow: 1;
  /* Flessibilità per far crescere lo spazio disponibile */
  display: flex;
  justify-content: flex-end;
  width: 60.63%;
  padding: 1rem;
  margin-right: 6rem;
}

.menu-items a {
  color: #b0b1b2;
  /* Colore del testo delle voci del menu */
  text-decoration: none;
}

.menu-items a:hover {
  border-bottom: 3px solid #27cdf2;
}
</style>
