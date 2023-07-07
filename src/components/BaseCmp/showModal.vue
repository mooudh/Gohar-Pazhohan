<template>
  <div class="modal-backdrop">
    <div class="modal">
      <header class="modal-header">
        <slot name="header"> نام و نام خانوادگی </slot>
      </header>
      <section class="modal-body" v-if="editMember">
        <slot name="body">
          <v-form @submit.prevent="submit" dir="rtl">
            {{ oneEmployee.id }}
            <base-form
              :FirstName="oneEmployee.firstName"
              :LastName="oneEmployee.lastName"
              :Email="oneEmployee.email"
              :BirthDay="oneEmployee.dateOfBirth"
            />

            <div>
              <p>تعداد اعضای خانواده : {{ FamilyNumber }} نفر</p>
              <sub-form
                v-for="i in FamilyNumber"
                :key="i"
                :FamilyMembers="FamilyMembers(i)"
                @removeSubMember="remove($event)"
              />
            </div>
            <v-btn class="me-4" color="secondary" type="submit"> تغییرات</v-btn>
          </v-form>
        </slot>
      </section>
      <footer class="modal-footer">
        <slot name="footer"> </slot>
        <button type="button" class="btn-blue" @click="editFunction">
          {{ editMember ? "ثبت" : "ویرایش" }}
        </button>
        <button type="button" class="btn-green" @click="close">
          Close Modal
        </button>
      </footer>
    </div>
  </div>
</template>
<script>
import BaseForm from "./baseForm.vue";
import SubForm from "./subForm.vue";
export default {
  components: { BaseForm, SubForm },

  props: ["oneEmployee"],

  data() {
    return {
      editMember: false,
      Employee: {},
    };
  },

  computed: {
    FamilyNumber() {
      if (this.oneEmployee.family) {
        return this.oneEmployee.family.length;
      }
    },
  },
  methods: {
    submit(submitEvent) {
      let firstName = submitEvent.target.elements.fname.value;
      let lastName = submitEvent.target.elements.lname.value;
      let email = submitEvent.target.elements.email1.value;
      let dateOfBirth = submitEvent.target.elements.birthday1.value;
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
      console.log(familyArray);
      this.Employee = {
        firstName: firstName,
        lastName: lastName,
        email: email,
        dateOfBirth: dateOfBirth,
        family: familyArray,
      };
      fetch(
        `https://goharp-task1.iran.liara.run/employee/${this.oneEmployee.id}`,
        {
          headers: {
            Authorization:
              "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d",
          },
          method: "PUT",
          body: this.Employee,
        }
      );
    },
    close() {
      this.$emit("close");
      this.editMember = false;
    },
    FamilyMembers(i) {
      return this.oneEmployee.family[i - 1];
    },

    remove(id) {
      if (confirm(`are you ${id}?`)) {
        console.log(id);
      }
    },
    editFunction() {
      if (this.editMember) {
        console.log(this.oneEmployee);
      } else {
      }
      this.editMember = !this.editMember;
    },
  },

  mounted() {
    console.log(this.oneEmployee);
  },
};
</script>
<style>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
}

.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  overflow-y: auto;
  max-height: 700px;
  display: flex;
  flex-direction: column;
  min-width: 600px !important;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  color: #4aae9b;
  justify-content: space-between;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
  justify-content: flex-end;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}
</style>
