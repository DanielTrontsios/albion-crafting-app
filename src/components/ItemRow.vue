<template>
  <v-expansion-panel-title>
    <v-row align="center" class="spacer" no-gutters>
      <v-col cols="4" md="1" sm="2">
        <v-avatar
          :image="itemInfo.avatarImg"
          :rounded="itemInfo.avatarRounded"
          :size="itemInfo.avatarSize"
          style="border: 0"
          class="mr-2"
        ></v-avatar>
        <strong> {{ itemInfo.message }} </strong>
      </v-col>

      <v-col>
        <v-text-field
          v-model="productPriceLocal"
          label="Product Price"
          type="number"
          required
        ></v-text-field>
      </v-col>

      <v-col>
        <v-text-field
          v-model="artifactPriceLocal"
          label="Artifact Price"
          type="number"
          required
        ></v-text-field>
      </v-col>

      <v-col class="text-no-wrap text-left" cols="5" sm="3">
        <v-card
          :title="profitTotal.toLocaleString('en-US')"
          subtitle="Profit Total"
        ></v-card>
      </v-col>

      <v-col class="hidden-sm-and-down">
        <v-card
          :title="profitPerItem.toLocaleString('en-US')"
          subtitle="Profit Per Item"
        ></v-card>
      </v-col>
    </v-row>
  </v-expansion-panel-title>

  <v-expansion-panel-text>
    <ArmorDisplay
      :resourceCostPerItem="resourceCostPerItem"
      :resourceCostTotal="resourceCostTotal"
      :profitPerItem="profitPerItem"
      :profitTotal="profitTotal"
      :feePerItem="feePerItem"
      :feeTotal="feeTotal"
    />
  </v-expansion-panel-text>
</template>

<script>
export default {
  props: {
    formData: {
      type: Object,
      required: true,
    },
    itemInfo: {
      type: Object,
      required: true,
    },
  },
  data: () => ({ artifactPriceLocal: 0, productPriceLocal: 0 }),
  computed: {
    resourceCostPerItem() {
      return (
        this.itemInfo.resourcesPer * this.formData.resourcePrice +
        this.itemInfo.artifactsPer * this.artifactPriceLocal
      );
    },
    resourceCostTotal() {
      return this.resourceCostPerItem * this.formData.numberOfItemsToCraft;
    },
    feePercent() {
      return this.formData.feePer100 / 44.444444;
    },
    feePerItem() {
      return Math.round(this.feePercent * this.formData.itemValue * (5 / 100));
    },
    feeTotal() {
      return this.feePerItem * this.formData.numberOfItemsToCraft;
    },
    profitPerItem() {
      return Math.round(
        this.productPriceLocal -
          this.resourceCostPerItem +
          (this.resourceCostPerItem / 100) * this.formData.returnRate -
          this.feePerItem
      );
    },
    profitTotal() {
      return this.profitPerItem * this.formData.numberOfItemsToCraft;
    },
  },
};
</script>
