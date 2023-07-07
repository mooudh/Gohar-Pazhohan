<template>
  <div>
    <div class="flex">
      <v-btn class="me-4 mb-4" @click="remove(info2.name)"> remove </v-btn>

      <v-text-field
        v-model="info2.name"
        name="memName"
        class="pa-2"
        label=" نام و نام خانوادگی"
        ref="name"
      ></v-text-field>

      <v-text-field
        v-model="info2.dateOfBirth"
        name="memBirthday"
        type="date"
        class="pa-2"
        label="تاریخ تولد"
        ref="date"
      ></v-text-field>
    </div>

    <v-select
      v-model="info2.relation"
      name="memRelation"
      :items="items"
      label="Select"
      placeholder="ddd"
      ref="item"
    ></v-select>
  </div>
</template>

<script>
export default {
  props: ["FamilyMembers"],
  data() {
    return {
      items: ["son", "daughter", "spouse"],
      info2: {
        name: "",
        dateOfBirth: "",
        relation: "نسبت خانوادگی",
      },
    };
  },

  methods: {
    remove(id) {
      this.$emit("removeSubMember", id);
    },
  },

  computed: {
    FullName() {
      if (this.FamilyMembers) {
        const fullName = this.FamilyMembers.name;
        return fullName.replace("-", " ");
      }
    },
    BirDay() {
      if (this.FamilyMembers) {
        const dateOfBirth = this.FamilyMembers.dateOfBirth;
        return dateOfBirth.substr(0, 10);
      }
    },
  },

  // created() {
  //   this.info2.name = this.FullName;
  //   if (this.FamilyMembers) this.info2.relation = this.FamilyMembers.relation;
  //   this.info2.dateOfBirth = this.BirDay;
  //   this.$emit("info3", this.info2);
  // },
};
</script>

<style scoped>
.flex {
  display: flex;
  padding: 10px;
}
</style>
