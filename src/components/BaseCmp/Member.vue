<template>
  <div>
    <v-form @submit.prevent="submit" dir="rtl">
      <div class="flex">
        <v-text-field
          v-model="FirstName"
          name="fname"
          class="pa-2"
          label="نام"
        ></v-text-field>

        <v-text-field
          v-model="LastName"
          name="lname"
          class="pa-2"
          label="نام خانوادگی"
        ></v-text-field>
      </div>

      <div class="flex">
        <v-text-field
          v-model="Email"
          name="email1"
          class="pa-2"
          label="ایمیل"
        ></v-text-field>

        <v-text-field
          v-model="BirthDay"
          name="birthday1"
          type="date"
          class="pa-2"
          label="تاریخ تولد"
        ></v-text-field>
      </div>
      <div>
        <v-btn class="me-4 mb-4" type="submit" @click.prevent="addMember">
          افزودن عضو خانواده</v-btn
        >
        <sub-member @subMember="info5($event)" v-if="showSubMember" />
      </div>

      <v-btn class="me-4" color="secondary" type="submit"> افزودن کارمند</v-btn>
    </v-form>
  </div>
</template>

<script>
import SubMember from "./SubMember.vue";
export default {
  components: { SubMember },
  data() {
    return {
      FirstName: "",
      LastName: "",
      Email: "",
      BirthDay: "",
      showSubMember: false,
      member: "",
      family: null,
    };
  },

  methods: {
    submit() {
      const firstName = this.FirstName;
      const lastName = this.LastName;
      const email = this.Email;
      const dateOfBirth = this.BirthDay;
      const family = this.family;
      this.member = {
        firstName: firstName,
        lastName: lastName,
        email: email,
        dateOfBirth: dateOfBirth,
        family: family,
      };
      console.log(this.member);

      fetch("https://goharp-task1.iran.liara.run/employee", {
        method: "POST",
        headers: {
          Authorization:
            "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d",
        },
        body: this.member,
      });
    },
    addMember() {
      this.showSubMember = true;
    },
    info5(mes) {
      this.family = mes;
      alert("ثبت انجام شد");
      console.log(this.family);
    },
  },
};
</script>

<style scoped>
.flex {
  display: flex;
  padding: 10px;
  min-width: 600px;
}
</style>
