<template>
  <v-app>
    <v-main>
      <v-card>
        <v-card-title>
          jsDelivr
          <v-spacer></v-spacer>

          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
        </v-card-title>

        <v-data-table
          class="elevation-1 table"
          :headers="npmHeaders"
          :items="npm"
          :search="search"
        >
          <template v-slot:item.name="props" 
            v-bind:selectName="this.selectName"
            v-bind:selectNPM="this.selectNpm"
          >
            <v-dialog v-model="dialog" width="500">
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  text
                  v-on="on"
                  v-bind="attrs"
                  v-on:click="get(props.item.name)"
                >
                  {{ props.item.name }}
                </v-btn>
              </template>

              <v-card>
                <v-card-title class="headline grey lighten-2">
                  {{ props.item.name }} - вот последний елемент в таблице
                </v-card-title>

                <v-card-text>
                  Простите отобразить уже не успела. Есть ошибка в коде, но не смогла найти
                </v-card-text>
              </v-card>
            </v-dialog>
          </template>
        </v-data-table>
      </v-card>

      <FooterPage />
    </v-main>
  </v-app>
</template>

<script>
import FooterPage from "./components/FooterPage";

export default {
  name: "App",

  components: {
    // HelloWorld,
    FooterPage,
  },

  data: () => ({
    npm: [],
    search: "",
    npmHeaders: [
      {
        text: "Hits",
        align: "start",
        value: "hits",
      },
      { text: "Name", value: "name" },
      { text: "Type", value: "type" },
    ],
    selectNpm: null,
    selectName: "npm name",
    dialog: false,
  }),
  methods: {
    get: function (name) {
      console.log(name);
      this.selectName = name;
      fetch("https://data.jsdelivr.com/v1/package/npm/" + name + "/stats")
        .then((response) => response.json())
        .then((json) => {
          console.log(json)
          this.selectNpm = json;
         
        });
        setTimeout(() => console.log(this.selectNpm), 1000)
    },
  },
  mounted() {
    fetch("https://data.jsdelivr.com/v1/stats/packages")
      .then((response) => response.json())
      .then((json) => {
        this.npm = json.filter((item) => item.type === "npm");
      });
  },
};
</script>
<style>
  .table {
    padding-bottom: 120px;
  }
 
</style>





// Smile =^_^=
