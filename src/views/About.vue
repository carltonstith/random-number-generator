<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-list dense>
        <v-list-item link to="/">
          <v-list-item-action>
            <v-icon>mdi-home</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link :to="{name:'contact'}">
          <v-list-item-action>
            <v-icon>mdi-contact-mail</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Contact</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link :to="{name:'about'}">
          <v-list-item-action>
            <v-icon>mdi-information-outline</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>About</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="indigo"
      dark
      class="blue-gradient"
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>
        <h1 class="logo">Lucky Number</h1>
      </v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <v-col class="text-center">
            
            <!-- About the application -->
            <div class="random-quote" col="6" sm="6" md="6">
              <i>{{ quote.content }}</i><br>
              <i>~{{ quote.author }}</i>
            </div>
            <div class="instructions">
              <p>Random numbers have many uses in science, art, statistics, cryptography, gaming, gambling, and other fields. For example, random assignment in randomized controlled trials helps scientists to test hypotheses, and random numbers or pseudorandom numbers help video games such as video poker.</p>
              <p>Use this application as you wish.</p>
            </div>
  
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import axios from 'axios'
  export default {
    name: 'LuckyNumber',
    props: {
      source: String,
    },

    data: () => ({
      drawer: null,
      quote: []
    }),

    mounted() {
      axios
        .get('https://api.quotable.io/random')
        .then(response => (this.quote = response.data))
    },

    created: function() {
      
    },

    methods: {
      
    },
  }
</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Open+Sans|Roboto&display=swap');

h1, h3 {
  font-family: 'Open Sans', sans-serif;
}
p {
  font-family: 'Roboto', sans-serif;
}
.logo {
  font-size:calc(20px + 0.8vw);
}
.random-quote {
  margin: 20px 0;
  width: 75%;
  text-align: center;
  display: inline-block;
}
.instructions {
  margin: 20px 0;
  width: 75%;
  text-align: center;
  display: inline-block;
}
.margin-top15 {
  margin-top: 15px;
}
.margin-top20 {
  margin-top: 20px;
}
.margin-bottom20 {
  margin-bottom: 20px;
}
.blue-gradient {
  background-color: #21D4FD;
  background-image: linear-gradient(19deg, #21D4FD 0%, #B721FF 100%);
}
.purple {
  background-color: #a61dfb;
}
.v-card:not(.v-sheet--tile):not(.v-card--shaped) {
  box-shadow: 0 1px 2px rgba(0,0,0,0.07), 
              0 2px 4px rgba(0,0,0,0.07), 
              0 4px 8px rgba(0,0,0,0.07), 
              0 8px 16px rgba(0,0,0,0.07),
              0 16px 32px rgba(0,0,0,0.07), 
              0 32px 64px rgba(0,0,0,0.07);
}
.v-btn.border-radius30 {
  border-radius: 30px;
}
</style>