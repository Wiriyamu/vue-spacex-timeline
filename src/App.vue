<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <h2>SpaceX</h2>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <v-main>
        <v-timeline v-if="launches.length > 0">
          <LaunchTimeLineItem
            v-for="launch in launches"
            :key="launch.flight_number"
            :launch="launch"
          />
        </v-timeline>
      </v-main>
    </v-content>
  </v-app>
</template>

<script>
import LaunchTimeLineItem from '@/components/LaunchTimeLineItem.vue';
export default {
  name: 'App',
  components: {
    LaunchTimeLineItem
  },
  data: () => ({
    launches: []
  }),
  async created() {
    const { data } = await this.$http('/launches')
    return this.launches = data
  }
};
</script>
