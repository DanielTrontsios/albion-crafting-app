<!-- eslint-disable vue/valid-v-slot -->
<template>
  <v-data-table :headers="headers" :items="items">
    <!-- Editable Calories Column -->
    <template v-slot:item.productPrice="{ item }">
      <v-text-field
        v-model="item.productPrice"
        type="number"
        min="0"
        class="pa-0 ma-0"
        hide-details
        solo
      ></v-text-field>
    </template>
    <template v-slot:item.artifactPrice="{ item }">
      <v-text-field
        v-model="item.artifactPrice"
        type="number"
        min="0"
        class="pa-0 ma-0"
        hide-details
        solo
      ></v-text-field>
    </template>
    <template v-slot:item.itemValue="{ item }">
      <v-text-field
        v-model="item.itemValue"
        type="number"
        min="0"
        class="pa-0 ma-0"
        hide-details
        solo
      ></v-text-field>
    </template>
    <template v-slot:item.profitTotal="{ item }">
      <v-chip :color="getColor(item)">
        {{ Math.round(getProfitTotal(item)).toLocaleString("en-US") }}
      </v-chip>
    </template>
    <template v-slot:item.profitPerItem="{ item }">
      <v-chip :color="getColor(item)">
        {{ Math.round(getProfitPerItem(item)).toLocaleString("en-US") }}
      </v-chip>
    </template>
    <template v-slot:item.resouceCostPerItem="{ item }">
      <v-chip>
        {{ Math.round(getResourceCostPerItem(item)).toLocaleString("en-US") }}
      </v-chip>
    </template>
    <template v-slot:item.craftingFeePerItem="{ item }">
      <v-chip>
        {{ Math.round(getCraftingFeePerItem(item)).toLocaleString("en-US") }}
      </v-chip>
    </template>
    <template v-slot:item.setupFeePerItem="{ item }">
      <v-chip>
        {{ Math.round(getSetupFeePerItem(item)).toLocaleString("en-US") }}
      </v-chip>
    </template>
  </v-data-table>
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
      required: false,
    },
  },
  data: () => ({
    headers: [
      { title: "Item", key: "name" },
      { title: "Product Price", key: "productPrice" },
      { title: "Artifact Price", key: "artifactPrice" }, // New column
      { title: "Item Value", key: "itemValue" }, // New column
      { title: "Profit Total", key: "profitTotal" },
      { title: "Profit Per Item", key: "profitPerItem" },
      { title: "Resource Cost Per Item", key: "resouceCostPerItem" },
      { title: "Crafting Fee Per Item", key: "craftingFeePerItem" },
      { title: "Setup Fee Per Item", key: "setupFeePerItem" },
    ],
    items: [
      {
        name: "Soldier Helmet",
        resourcesPer: 8,
        artifactsPer: 0,
        productPrice: 1331,
        artifactPrice: 0,
        itemValue: 128,
      },
      {
        name: "Knight Helmet",
        resourcesPer: 8,
        artifactsPer: 0,
        productPrice: 1332,
        artifactPrice: 0,
        itemValue: 128,
      },
      {
        name: "Guardian Helmet",
        resourcesPer: 8,
        artifactsPer: 0,
        productPrice: 1319,
        artifactPrice: 0,
        itemValue: 128,
      },
      {
        name: "Royal Helmet",
        resourcesPer: 8,
        artifactsPer: 2,
        productPrice: 91025,
        artifactPrice: 29059,
        itemValue: 160,
      },
      {
        name: "Graveguard Helmet",
        resourcesPer: 8,
        artifactsPer: 1,
        productPrice: 2422,
        artifactPrice: 597,
        itemValue: 160,
      },
      {
        name: "Demon Helmet",
        resourcesPer: 8,
        artifactsPer: 1,
        productPrice: 7413,
        artifactPrice: 1607,
        itemValue: 224,
      },
      {
        name: "Judicator Helmet",
        resourcesPer: 8,
        artifactsPer: 1,
        productPrice: 26948,
        artifactPrice: 10701,
        itemValue: 352,
      },
      {
        name: "Duskweaver Helmet",
        resourcesPer: 8,
        artifactsPer: 1,
        productPrice: 17841,
        artifactPrice: 3873,
        itemValue: 352,
      },
      {
        name: "Helmet of Valor",
        resourcesPer: 8,
        artifactsPer: 1,
        productPrice: 78744,
        artifactPrice: 47691,
        itemValue: 608,
      },
    ],
  }),
  computed: {
    feePercent() {
      return this.formData.feePer100 / 44.444444;
    },
  },
  methods: {
    getColor(item) {
      const totalProfit = this.getProfitTotal(item);
      const totalCost = this.getResourceCostTotal(item);
      if (totalProfit < 0) return "red";
      else if (totalProfit < totalCost * 0.05) return "orange";
      else return "green";
    },
    getCraftingFeePerItem(item) {
      return this.feePercent * item.itemValue * 0.05;
    },
    getSetupFeePerItem(item) {
      return item.productPrice * 0.65;
    },
    getResourceCostPerItem(item) {
      return (
        (item.resourcesPer -
          item.resourcesPer * (this.formData.returnRate / 100)) *
          this.formData.resourcePrice +
        item.artifactsPer * item.artifactPrice
      );
    },
    getResourceCostTotal(item) {
      return (
        this.getResourceCostPerItem(item) * this.formData.numberOfItemsToCraft
      );
    },
    getProfitPerItem(item) {
      const resourceCostPerItem = this.getResourceCostPerItem(item);
      return (
        item.productPrice -
        resourceCostPerItem -
        this.getCraftingFeePerItem(item) -
        item.productPrice * 0.65
      );
    },
    getProfitTotal(item) {
      return this.getProfitPerItem(item) * this.formData.numberOfItemsToCraft;
    },
  },
};
</script>
