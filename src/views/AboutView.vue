<template>
  <div>
    <div class="text-subtitle-2 mt-4 mb-2">کارمندان</div>
    <p v-if="employees.length == 0">نامی برای نمایش داده شدن وجود ندارد</p>
    <v-expansion-panels variant="inset" class="my-4" v-else>
      <v-expansion-panel
        v-for="i in employees"
        :key="i"
        :title="fullName(i.id)"
        @click="showModal(i.id)"
      >
      </v-expansion-panel>
    </v-expansion-panels>

    <show-modal
      v-show="isModalVisible"
      @close="closeModal"
      :oneEmployee="oneEmployee"
    >
      <template v-slot:header>
        <div>
          {{ oneEmployee ? oneEmployee.firstName : "" }}
          {{ oneEmployee ? oneEmployee.lastName : "" }}
        </div>
        <p>
          ایمیل:
          {{ oneEmployee ? oneEmployee.email : "" }}
        </p>
        <div>
          سال تولد:
          {{ oneEmployee ? oneEmployee.dateOfBirth : "" }}
        </div>
      </template>

      ></show-modal
    >
    <del-modal />
  </div>
</template>

<script>
import AddModal from "../components/BaseCmp/addModal.vue";
import DelModal from "../components/BaseCmp/DelModal.vue";
import ShowModal from "../components/BaseCmp/showModal.vue";

export default {
  components: {
    DelModal,
    ShowModal,
    AddModal,
  },
  data() {
    return {
      modal: false,
      isModalVisible: false,
      isAddModalVisible: false,
      employees: [],
      oneEmployee: {},
    };
  },

  methods: {
    fetch() {
      fetch("https://goharp-task1.iran.liara.run/employee", {
        headers: {
          Authorization:
            "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d",
        },
      })
        .then((data) => data.json())
        .then((response) => {
          this.employees = response;
        });
    },

    fullName(id) {
      let employee = this.employees.filter((item) => item.id == id);
      return `${employee[0].firstName} ${employee[0].lastName}`;
    },

    showModal(id) {
      this.isModalVisible = true;
      fetch(`https://goharp-task1.iran.liara.run/employee/${id}`, {
        headers: {
          Authorization:
            "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d",
        },
      })
        .then((data) => data.json())
        .then((response) => {
          this.oneEmployee = response;
        });
    },
    closeModal() {
      this.isModalVisible = false;
      this.oneEmployee = {};
      this.fetch();
    },
  },

  created() {
    this.fetch();
  },
};
</script>
