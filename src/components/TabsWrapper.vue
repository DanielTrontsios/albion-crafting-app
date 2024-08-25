<template>
  <v-card>
    <v-tabs v-model="tab" bg-color="primary">
      <v-tab value="one">Cloth</v-tab>
      <v-tab value="two">Hide</v-tab>
      <v-tab value="three">Plate</v-tab>
    </v-tabs>

    <v-card-text>
      <v-tabs-window v-model="tab">
        <v-tabs-window-item value="one"> Cloth </v-tabs-window-item>

        <v-tabs-window-item value="two"> Hide </v-tabs-window-item>

        <v-tabs-window-item value="three">
          <PlateTab />
        </v-tabs-window-item>
      </v-tabs-window>
    </v-card-text>
  </v-card>
</template>
<script>
export default {
  data: () => ({
    tab: null,
  }),
};
</script>
