<template>
  <v-expansion-panels multiple>
    <v-expansion-panel>
      <v-expansion-panel-title>
        <div>
          <v-avatar
            :image="helmetInfo.avatarImg"
            :rounded="helmetInfo.avatarRounded"
            :size="helmetInfo.avatarSize"
            style="border: 0"
            class="mr-2"
          ></v-avatar>
          <strong> {{ helmetInfo.message }}</strong>
        </div>
      </v-expansion-panel-title>
      <v-expansion-panel-text>
        <ArmorForm />
      </v-expansion-panel-text>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-title>
        <div>
          <v-avatar
            :image="chestInfo.avatarImg"
            :rounded="chestInfo.avatarRounded"
            :size="chestInfo.avatarSize"
            style="border: 0"
            class="mr-2"
          ></v-avatar>
          <strong> {{ chestInfo.message }} </strong>
        </div>
      </v-expansion-panel-title>
      <v-expansion-panel-text>
        <ArmorForm />
      </v-expansion-panel-text>
    </v-expansion-panel>
    <v-expansion-panel>
      <v-expansion-panel-title>
        <div>
          <v-avatar
            :image="bootsInfo.avatarImg"
            :rounded="bootsInfo.avatarRounded"
            :size="bootsInfo.avatarSize"
            style="border: 0"
            class="mr-2"
          ></v-avatar>
          <strong> {{ bootsInfo.message }} </strong>
        </div>
      </v-expansion-panel-title>
      <v-expansion-panel-text>
        <ArmorForm />
      </v-expansion-panel-text>
    </v-expansion-panel>
  </v-expansion-panels>
</template>
<script>
export default {
  data: () => ({
    helmetInfo: {
      avatarImg: "https://render.albiononline.com/v1/item/T4_HEAD_PLATE_SET1",
      avatarSize: 65,
      avatarRounded: 0,
      message: "Helmet",
    },
    chestInfo: {
      avatarImg: "https://render.albiononline.com/v1/item/T4_ARMOR_PLATE_SET1",
      avatarSize: 65,
      avatarRounded: 0,
      message: "Armor",
    },
    bootsInfo: {
      avatarImg: "https://render.albiononline.com/v1/item/T4_SHOES_PLATE_SET1",
      avatarSize: 65,
      avatarRounded: 0,
      message: "Boots",
    },
  }),
};
</script>
