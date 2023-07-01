<template>
  <div>
    <div class="text-subtitle-2 mt-4 mb-2">کارمندان</div>
    <p v-if="employee.length == 0">نامی برای نمایش داده شدن وجود ندارد</p>
    <v-expansion-panels variant="inset" class="my-4" v-else>
      <v-expansion-panel
        v-for="i in employee"
        :key="i"
        :title="fullName(i.id)"
      ></v-expansion-panel>
    </v-expansion-panels>

    <del-modal />
  </div>
</template>

<script>
import axios from "axios";
import DelModal from "../components/BaseCmp/DelModal.vue";

export default {
  components: {
    DelModal,
  },
  data() {
    return {
      modal: false,
      dialog: false,

      employee: [
        {
          firstName: "محمد",
          lastName: "رحیمی",
          id: "550b0ea7-c485-4ac0-89aa-6142467d7532",
        },
        {
          firstName: "علی",
          lastName: "محمدی",
          id: "550b0ea7-c485-4ac0-89aa-617746417532",
        },
        {
          firstName: "پوریا",
          lastName: "خاقانی",
          id: "550b0ea7-c485-4ac0-89aa-6177467d7532",
        },
      ],
      // employee: [],
    };
  },

  methods: {
    fullName(id) {
      let employee = this.employee.filter((item) => item.id == id);
      return `${employee[0].firstName} ${employee[0].lastName}`;
    },
    showmodal() {
      this.modal = true;
    },
    hidemodal() {
      this.modal = false;
    },
  },

  mounted() {
    // var myHeaders = new Headers();
    // myHeaders.append(
    //   "Authorization",
    //   "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d"
    // );

    // var requestOptions = {
    //   method: "GET",
    //   headers: myHeaders,
    //   redirect: "follow",
    //   mode: "no-cors",
    //   Accept: "application/json",
    //   "Access-Control-Allow-Origin": "*",
    //   "Access-Control-Allow-Credentials": true,
    // };

    // fetch("https://goharp-task1.iran.liara.run/employee", requestOptions).then(
    //   (res) => this.employee.push(res)
    // );

    var config = {
      method: "get",
      url: "https://goharp-task1.iran.liara.run/employee",
      headers: {
        "Access-Control-Allow-Origin": "http://localhost:5173/",
        Authorization:
          "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d",
      },
      mode: "no-cors",
    };

    axios(config)
      .then(function (response) {
        console.log(JSON.stringify(response.data));
      })
      .catch(function (error) {
        console.log(error);
      });
  },
  // .then((response) => response.text())
  // .catch((error) => console.log("error", error));
  // },
  //   fetch("https://goharp-task1.iran.liara.run/employee", {
  //     headers: {
  //       "Access-Control-Allow-Origin": "http://localhost:5173/",
  //       Authorization:
  //         "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d",
  //     },
  //     mode: "no-cors",
  //   })
  //     .then((data) => data.json())
  //     .then((response) => console.log(response));
  // },

  // axios
  //   .get("https://goharp-task1.iran.liara.run/employee", {
  //     headers: {
  //       "Access-Control-Allow-Origin": "http://localhost:5173",
  //       "Access-Control-Allow-Credentials": true,
  //       "Content-Type": "application/json",
  //       Authorization:
  //         "Bearer mooud-hoseini-61162158-1dc3-489d-890e-864556e58b4d",
  //     },
  //   })
  //   .then((response) => console.log(response));
};
</script>
