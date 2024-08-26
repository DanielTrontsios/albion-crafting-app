<template>
  <ArmorForm :initialData="formData" @update-data="updateData" />

  <v-expansion-panels multiple>
    <v-expansion-panel>
      <ItemRow :formData="formData" :itemInfo="helmetInfo" />
    </v-expansion-panel>
    <v-expansion-panel>
      <ItemRow :formData="formData" :itemInfo="chestInfo" />
    </v-expansion-panel>
    <v-expansion-panel>
      <ItemRow :formData="formData" :itemInfo="bootsInfo" />
    </v-expansion-panel>
  </v-expansion-panels>
</template>
<script>
export default {
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
    helmetInfo: {
      avatarImg: "https://render.albiononline.com/v1/item/T4_HEAD_PLATE_SET1",
      avatarSize: 65,
      avatarRounded: 0,
      message: "Helmet",
      resourcesPer: 8,
      artifactsPer: 1,
    },
    chestInfo: {
      avatarImg: "https://render.albiononline.com/v1/item/T4_ARMOR_PLATE_SET1",
      avatarSize: 65,
      avatarRounded: 0,
      message: "Armor",
      resourcesPer: 16,
      artifactsPer: 1,
    },
    bootsInfo: {
      avatarImg: "https://render.albiononline.com/v1/item/T4_SHOES_PLATE_SET1",
      avatarSize: 65,
      avatarRounded: 0,
      message: "Boots",
      resourcesPer: 8,
      artifactsPer: 1,
    },
  }),
  computed: {
    resourcesPer() {
      return 8;
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
