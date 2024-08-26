<template>
  <v-form v-model="valid">
    <v-container fluid>
      <v-row>
        <v-col cols="12" md="3">
          <v-text-field
            v-model="localData.resourcePrice"
            label="Resource Price"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            v-model="localData.feePer100"
            label="Fee Per 100"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            v-model="localData.returnRate"
            label="Return Rate"
            type="number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="3">
          <v-text-field
            v-model="localData.numberOfItemsToCraft"
            label="Number Of Items To Craft"
            type="number"
            required
          ></v-text-field>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  props: {
    initialData: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      valid: false,
      localData: { ...this.initialData },
    };
  },
  watch: {
    localData: {
      deep: true,
      handler(newVal) {
        this.$emit("update-data", newVal);
      },
    },
  },
};
</script>
