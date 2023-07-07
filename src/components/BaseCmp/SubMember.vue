<template>
  <div>
    <v-form @submit.prevent="submit" dir="rtl">
      <div v-for="i in num" :key="i">
        <sub-form @info3="func($event, i)" @removeSubMember="remove($event)" />
      </div>
      <div>
        <v-btn class="me-4 mb-4" type="submit" @click="createForm"> + </v-btn>
        <v-btn
          class="me-4 mb-4"
          type="submit"
          @click="removeForm"
          v-if="num > 0"
        >
          -
        </v-btn>
        <v-btn class="me-4 mb-4" type="submit" v-if="num > 0">
          ثبت اعضای خانواده</v-btn
        >
      </div>
      <!-- <v-btn @click="handleReset"> clear </v-btn> -->
    </v-form>
  </div>
</template>

<script>
import subForm from "./subForm.vue";
export default {
  components: { subForm },
  name: "SubMember",
  data() {
    return {
      // info: [{ id: 1, name: "", date: "", item: "" }],
      info4: [],
      num: 1,
    };
  },

  methods: {
    // this.$emit("subMember", this.info4);
    submit(submitEvent) {
      let familyArray = [];
      if (submitEvent.target.elements.memName.length > 0) {
        for (let i = 0; i < submitEvent.target.elements.memName.length; i++) {
          let name = submitEvent.target.elements.memName[i].value;
          let dateOfBirth = submitEvent.target.elements.memBirthday[i].value;
          let relation = submitEvent.target.elements.memRelation[i].value;
          familyArray.push({
            name: name,
            dateOfBirth: dateOfBirth,
            relation: relation,
          });
        }
      } else {
        let name = submitEvent.target.elements.memName.value;
        let dateOfBirth = submitEvent.target.elements.memBirthday.value;
        let relation = submitEvent.target.elements.memRelation.value;
        familyArray.push({
          name: name,
          dateOfBirth: dateOfBirth,
          relation: relation,
        });
      }
      // console.log(familyArray);
      this.$emit("subMember", familyArray);
      // this.Employee = {
      //   firstName: firstName,
      //   lastName: lastName,
      //   email: email,
      //   dateOfBirth: dateOfBirth,
      //   family: familyArray,
      // };
      // fetch(
      //   `https://goharp-task1.iran.liara.run/employee/${this.oneEmployee.id}`,
      //   {
      //     headers: {
      //       Authorization:
      //         "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d",
      //     },
      //     method: "PUT",
      //     body: this.Employee,
      //   }
      // );
    },
    createForm() {
      this.num++;
    },
    removeForm() {
      this.num--;
    },
    func(event, id) {
      const obj1 = event;
      event["id"] = id;
      this.info4.push(obj1);
    },
    remove(id) {
      this.removeForm();
      this.info4.splice(id - 1, 1);
    },
  },

  computed: {
    length() {
      return this.info.length;
    },
  },
};
</script>

<style scoped></style>
