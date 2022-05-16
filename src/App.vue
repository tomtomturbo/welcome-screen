<template>
  <body>
    
    <div id="app">
      <div class="header">
      <h1 style="text-align: left">Welcome to Opportunity</h1>
      <p class="currentTime">{{ currentDateTime() }}</p>
    </div>
      <ul>
        <li class="li">
          <span class="entry-daytime">12.00 Uhr</span>
          <h3>Basisbeschäftigung Besuch</h3>
          <span class="entry-description">erster Eintrag </span>
        </li>
        <li class="li">
          <span class="entry-daytime">14.00 Uhr </span>
          <h3>Basisbeschäftigung Besuch 2</h3>
            <span class="entry-description">nächster Eintrag </span>
        </li>
        <li class="li">
          <span class="entry-daytime">16.00 Uhr</span>
          <h3>Basisbeschäftigung Besuch X</h3>
          <span class="entry-description">letzter Eintrag</span>
        </li>
      </ul>

    <footer>
<img class="img" src="./assets/STZH_SEB_Logo.png"
/>
<img class="img" src="./assets/Opportunity.png"
/>
<img class="img" src="./assets/SAG_Logo_De.png"
/>

    </footer>

  
    </div>
  </body>

</template>

<script>
export default {
  name: "App",
  methods: {
    currentDateTime() {
      const current = new Date();
      const date =
        current.getDate() +
        "." +
        (current.getMonth() + 1) +
        "." +
        current.getFullYear();
      return date;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;900&display=swap");
body {
  margin: 0;
  font-family: 'Inter', Helvetica, sans-serif;
  background-position: center;
  background-size: cover;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 100vh;
  font-size: 28px;
  line-height: 36px;

}
#app {
}
.li {
  list-style-type: none;
  background-color: #0F05A0;
  color:#ffbfab;
  margin: 2rem;
  padding: 2rem;
 
}
.entry-daytime {
  color: #EB5E00;
  font-weight: 900;
  font-size: 28px;
  line-height: 10px;

}
.header {
 
  margin-left: 4.5rem;
  margin-right: 2rem;
  text-align: left;
  font-size: small;

  }

.currentTime{
font-size: 28px;
font-weight: 900;
}
.img{
  width: 20%;
}
</style>