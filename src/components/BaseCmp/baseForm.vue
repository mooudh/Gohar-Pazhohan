<template>
  <div>
    <div class="flex">
      <v-text-field
        v-model="FirstName1"
        class="pa-2"
        label="نام"
        name="fname"
      ></v-text-field>

      <v-text-field
        v-model="LastName1"
        name="lname"
        class="pa-2"
        label="نام خانوادگی"
      ></v-text-field>
    </div>
    <div class="flex">
      <v-text-field
        v-model="Email1"
        name="email1"
        class="pa-2"
        label="ایمیل"
      ></v-text-field>

      <v-text-field
        v-model="BirthDay1"
        name="birthday1"
        type="date"
        class="pa-2"
        label="تاریخ تولد"
      ></v-text-field>
    </div>
  </div>
</template>

<script>
export default {
  props: ["FirstName", "LastName", "Email", "BirthDay"],
  data() {
    return {
      FirstName1: "",
      LastName1: "",
      Email1: "",
      BirthDay1: "",
    };
  },

  computed: {
    BirDay() {
      if (this.BirthDay) {
        return this.BirthDay.substr(0, 10);
      }
    },
  },

  mounted() {
    this.FirstName1 = this.FirstName;
    this.LastName1 = this.LastName;
    this.Email1 = this.Email;
    this.BirthDay1 = this.BirDay;
  },
};
</script>

<style scoped>
.flex {
  display: flex;
  padding: 10px;
}
</style>
