<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <!-- <span></span> -->
        <span class="font-weight-light">Departments</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      
    </v-app-bar>

    <v-content>
      <!-- <HelloWorld/> -->
      <ManageDept/>
    </v-content>
  </v-app>
</template>

<script>
import ManageDept from './components/ManageDept';
export default {
  name: 'App',
  components: {
    ManageDept,
  },
  data: () => ({
    //
  }),
};
</script>
