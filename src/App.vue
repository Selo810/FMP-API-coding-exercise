<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Kapitus Logo"
          class="shrink mr-2"
          contain
          src="https://www.magnifymoney.com/banklogos/kapituslogo.jpg"
          transition="scale-transition"
          width="100"
        />
      </div>

    </v-app-bar>

    <v-content>
      <CompanyPro/>
    </v-content>
  </v-app>
</template>

<script>
import CompanyPro from './components/CompanyPro';

export default {
  name: 'App',

  components: {
    CompanyPro
  },

  data: () => ({
    //
  }),
};
</script>
