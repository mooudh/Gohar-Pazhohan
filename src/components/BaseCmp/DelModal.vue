<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="auto">
      <template v-slot:activator="{ props }">
        <v-btn color="secondary" v-bind="props"> افزودن کارمند </v-btn>
      </template>

      <v-card>
        <v-card-text>
          <member />
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" block @click="dialog = false"
            >Close Dialog</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
import Member from "./Member.vue";

export default {
  components: {
    Member,
  },
  data() {
    return {
      dialog: false,
    };
  },
};
</script>
