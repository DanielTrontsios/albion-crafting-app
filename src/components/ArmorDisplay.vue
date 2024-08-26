<template>
  <v-container fluid>
    <v-row>
      <v-col>
        <v-card
          :title="profitTotal.toLocaleString('en-US')"
          subtitle="Profit Total"
        ></v-card>
      </v-col>
      <v-col>
        <v-card
          :title="profitPerItem.toLocaleString('en-US')"
          subtitle="Profit Per Item"
        ></v-card>
      </v-col>
      <v-col>
        <v-card
          :title="resourceCostTotal.toLocaleString('en-US')"
          subtitle="Resource Cost Total"
        ></v-card>
      </v-col>
      <v-col>
        <v-card
          :title="resourceCostPerItem.toLocaleString('en-US')"
          subtitle="Resource Cost Per Item"
        ></v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-card
          :title="feeTotal.toLocaleString('en-US')"
          subtitle="Fee Total"
        ></v-card>
      </v-col>
      <v-col>
        <v-card
          :title="feePerItem.toLocaleString('en-US')"
          subtitle="Fee Per Item"
        ></v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: {
    resourceCostPerItem: Number,
    resourceCostTotal: Number,
    profitPerItem: Number,
    profitTotal: Number,
    feePerItem: Number,
    feeTotal: Number,
  },
};
</script>
