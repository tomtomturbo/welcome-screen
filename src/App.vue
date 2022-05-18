<template>
  <body>
    <div id="app">
      <div class="header">
        <h1 style="text-align: left">{{ title }}</h1>
        <p class="currentTime">{{ currentDateTime() }}</p>
      </div>

      <ul v-if="entries" class="unorderedList">
        <li class="li" v-for="entry in entries" :key="entry.id">
          <span class="entry"
            >{{ entry[0].replace(":",".") }} , {{ entry[1].replaceAll("/", ".") }}</span
          ><br />
          <h3>{{ entry[2] }}</h3>
          <span class="thirdLine">{{ entry[3] }}</span
          ><br />
        </li>
      </ul>

      <p class="sentence" v-else>keine Einträge</p>

      <footer>
        <img class="img" src="./assets/STZH_SEB_Logo.png" />
        <img class="img" src="./assets/Opportunity.png" />
        <img class="img" src="./assets/SAG_Logo_De.png" />
      </footer>
    </div>
  </body>
</template>

<script>
import axios from "axios"; //axios is a library for making HTTP requests to the backend

export default {
  name: "App",
  data() {
    return {
      title: "Welcome to Opportunity",
      sheet_id: "1a81aI0Y8ViZO0tI92h2YSMqVQJ8hmNNMyMylXgvwiU4",
      api_token: "AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU",
      entries: [],
      dateTime: "",
    };
  },

  computed: {
    gsheet_url() {
      return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE200&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
    },
  },
  methods: {
    currentDateTime() {
      const current = new Date();
      const day = current.getDate();
      const month = current.getMonth() + 1;
      const year = current.getFullYear();

      const dateTime = day + "." + month + "." + year;

      if (month < 10) {
        return day + "." + "0" + month + "." + year;
      }
      return dateTime;
    },
    getData() {
      axios.get(this.gsheet_url).then((response) => {
        this.entries = response.data.valueRanges[0].values;
        console.log(this.entries);
      });
    },
    refreshData() {
      this.currentDateTime();
      this.getData();
    },
  },
  mounted() {
    this.refreshData();
    setInterval(this.refreshData, 1000 * 60 * 30);
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&display=swap");
body {
  margin: 0;
  font-family: "Inter", Helvetica, sans-serif;
  background-position: center;
  background-size: cover;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 100vh;
  font-size: 24px;
  line-height: 36px;
  background-color: #e5e5e5;
}

.li {
  list-style-type: none;
  background-color: #0f05a0;
  color: #ffbfab;
  margin: 1.5rem;
  padding: 2.5rem;
  line-height: 20px;
}
/* .unorderedList {
  line-height: 2rem;
  margin-right: 2rem;
  margin-left: 0.5rem;
} */

.header {
  margin-left: 4.5rem;
  text-align: left;
  font-size: 25px;
  line-height: 75px;
}

.currentTime {
  font-size: 48px;
  color: grey;
  line-height: 12px;
}
.img {
  width: 20%;
  margin-left: auto;
  margin-right: auto;
}

footer {
  display: flex;
  flex-wrap: wrap;
  padding-bottom: 10px;
  background-color: #ffffff;
  position: fixed;
  bottom: 0;
}

.entry {
  color: #eb5e00;
  font-size: 28px;
  font-weight: 900;
}
.thirdLine {
  font-weight: 400;
}
.sentence {
  margin-left: 80px;
  color: darkblue;
  font-weight: 900;
}
</style>


