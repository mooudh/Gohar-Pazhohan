<template>
  <div class="text-center">
    <v-btn color="secondary" @click="dialog = true"> افزودن کارمند </v-btn>

    <v-dialog v-model="dialog" width="800">
      <v-card>
        <v-card-text>
          <member></member>
        </v-card-text>
        <v-card-actions>
          <v-btn color="secondary" block @click="dialog = false"
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
