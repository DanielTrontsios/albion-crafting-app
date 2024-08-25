<template>
  <v-form v-model="valid">
    <v-container fluid>
      <v-row>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="resourcePrice"
            label="Resource Price"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="artifactPrice"
            label="Artifact Price"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="productPrice"
            label="Product Price"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="feePer100"
            label="Fee Per 100"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="itemValue"
            label="Item Value"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="4">
          <v-text-field
            v-model="returnRate"
            label="Return Rate"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12">
          <v-text-field
            v-model="numberOfItemsToCraft"
            label="Number Of Items To Craft"
            type="number"
            required
          ></v-text-field>
        </v-col>
      </v-row>
    </v-container>
    <v-container>
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
  </v-form>
</template>

<script>
export default {
  data: () => ({
    valid: false,
    resourcePrice: 277,
    artifactPrice: 4000,
    productPrice: 9100,
    feePer100: 600,
    itemValue: 448,
    returnRate: 33.8,
    numberOfItemsToCraft: 100,
    resourcesPer: 16,
    artifactsPer: 1,
  }),
  computed: {
    resourceCostPerItem() {
      return (
        this.resourcesPer * this.resourcePrice +
        this.artifactsPer * this.artifactPrice
      );
    },
    resourceCostTotal() {
      return this.resourceCostPerItem * this.numberOfItemsToCraft;
    },
    feePercent() {
      return this.feePer100 / 44.444444;
    },
    feePerItem() {
      return Math.round(this.feePercent * this.itemValue * (5 / 100));
    },
    feeTotal() {
      return this.feePerItem * this.numberOfItemsToCraft;
    },
    profitPerItem() {
      return Math.round(
        this.productPrice -
          this.resourceCostPerItem +
          (this.resourceCostPerItem / 100) * this.returnRate -
          this.feePerItem
      );
    },
    profitTotal() {
      return this.profitPerItem * this.numberOfItemsToCraft;
    },
  },
};
</script>
