<template>
  <div>
    <v-form @submit.prevent="submit" dir="rtl">
      <div class="flex">
        <v-text-field
          v-model="FirstName"
          class="pa-2"
          label="نام"
        ></v-text-field>

        <v-text-field
          v-model="LastName"
          class="pa-2"
          label="نام خانوادگی"
        ></v-text-field>
      </div>

      <div class="flex">
        <v-text-field v-model="Email" class="pa-2" label="ایمیل"></v-text-field>

        <v-text-field
          v-model="BirthDay"
          type="date"
          class="pa-2"
          label="تاریخ تولد"
        ></v-text-field>
      </div>

      <v-select
        v-model="select.value.value"
        :items="items"
        :error-messages="select.errorMessage.value"
        label="Select"
      ></v-select>

      <div>
        <v-btn class="me-4 mb-4" type="submit"> افزودن عضو خانواده</v-btn>
      </div>

      <v-btn class="me-4" type="submit"> افزودن </v-btn>

      <!-- <v-btn @click="handleReset"> clear </v-btn> -->
    </v-form>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped></style>
