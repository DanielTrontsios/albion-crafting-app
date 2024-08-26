<template>
  <FormComponent :initialData="formData" @update-data="updateData" />
  <DisplayComponent
    :resourceCostPerItem="resourceCostPerItem"
    :resourceCostTotal="resourceCostTotal"
    :profitPerItem="profitPerItem"
    :profitTotal="profitTotal"
    :feePerItem="feePerItem"
    :feeTotal="feeTotal"
  />
</template>

<script>
import FormComponent from "./FormComponent.vue";
import DisplayComponent from "./DisplayComponent.vue";

export default {
  components: {
    FormComponent,
    DisplayComponent,
  },
  data: () => ({
    formData: {
      resourcePrice: 277,
      artifactPrice: 4000,
      productPrice: 9100,
      feePer100: 600,
      itemValue: 448,
      returnRate: 33.8,
      numberOfItemsToCraft: 100,
    },
    artifactsPer: 1,
  }),
  computed: {
    resourcesPer() {
      return this.artifactsPer;
    },
    resourceCostPerItem() {
      return (
        this.resourcesPer * this.formData.resourcePrice +
        this.artifactsPer * this.formData.artifactPrice
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
        this.formData.productPrice -
          this.resourceCostPerItem +
          (this.resourceCostPerItem / 100) * this.formData.returnRate -
          this.feePerItem
      );
    },
    profitTotal() {
      return this.profitPerItem * this.formData.numberOfItemsToCraft;
    },
  },
  methods: {
    updateData(newData) {
      this.formData = newData;
    },
  },
};
</script>
