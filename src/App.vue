<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-row>
        <v-col cols="12" class="text-center">
          <h1>Student Dashboard</h1>
        </v-col>
      </v-row>
    </v-app-bar>

    <v-content>
      <Dashboard/>
    </v-content>
  </v-app>
</template>

<script>
import Dashboard from './components/Dashboard';

export default {
  name: 'App',

  components: {
    Dashboard,
  },

  data: () => ({
    //
  }),
};
</script>
