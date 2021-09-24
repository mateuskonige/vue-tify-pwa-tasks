<template>
  <v-app>
   <v-main>
      <v-container >
        <ListTasks/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import ListTasks from './components/Tasks/ListTasks.vue';

export default {
  name: 'App',

  components: {
    ListTasks,
  },

  data: () => ({
    //
  }),
};
</script>
