<template>
  <v-app id="inspire">
    <!-- <v-navigation-drawer
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
    </v-navigation-drawer> -->

    <!-- <v-app-bar
      app
      color="indigo"
      dark
      class="blue-gradient"
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>
        <h1 class="logo">Lucky Number</h1>
      </v-toolbar-title>
    </v-app-bar> -->

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
            <v-toolbar-title class="margin-top40 margin-bottom40">
              <h1 class="logo">Lucky Number</h1>
            </v-toolbar-title>
            <!-- Lucky Number Output -->
            <v-card
              class="mx-auto margin-bottom20"
              max-width="344"
              outlined
            >
            <div class="margin-top15">
              <p id="randomNum">{{ number }}</p>
            </div>

              <v-list-item three-line>

                <v-col cols="6" sm="6" md="6">
                  <v-text-field
                    label="Min"
                    solo
                    id="min" 
                    v-model="min" 
                    min="-9999999999" 
                    max="9999999999" 
                    type="number"
                  ></v-text-field>
                </v-col>

                <v-col cols="6" sm="6" md="6">
                  <v-text-field
                    label="Max"
                    solo
                    id="max" 
                    v-model="max" 
                    min="-9999999999" 
                    max="9999999999" 
                    type="number"
                  ></v-text-field>
                </v-col>
          
              </v-list-item>
          
              <v-card-actions class="margin-bottom15">
                <!-- <v-btn text @click="handleSave()">Save</v-btn>
                <v-btn text @click="handlePickAnotherNumber()">Pick Another Number</v-btn> -->
                <v-btn
                  class="margin-top20 border-radius30 randomNumberButton" 
                  @click="getInput"
                >Generate a Random Number</v-btn>
              </v-card-actions>
            </v-card>

            <v-btn text @click="handleSave()">Save</v-btn>
            <v-btn text @click="handlePickAnotherNumber()">Pick Another Number</v-btn> 

            <div class="random-quote" col="6" sm="6" md="6">
              <i>{{ quote.content }}</i><br>
              <i>~{{ quote.author }}</i>
            </div>

            <!-- <v-btn
              class="margin-top20 border-radius30" 
              @click="getInput"
            >Generate a Random Number</v-btn> -->
  
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
      min: '',
      max: '',
      number: 1,
      quote: []
    }),

    mounted() {
      axios
        .get('https://api.quotable.io/random')
        .then(response => (this.quote = response.data))
    },

    created: function() {
      this.getRandomNumber();
    },

    methods: {
      loadNum: function () {
        this.min = 1;
        this.max = 10;
        this.getRandomNumber();
      },

      getInput: function () {
        let min = Number(this.min)
        let max = Number(this.max)
        if(min > max) {
          [min, max] = [max, min]
        }
        this.min = min
        this.max = max
        this.getRandomNumber()

        axios
        .get('https://api.quotable.io/random')
        .then(response => (this.quote = response.data))
      },

      getRandomNumber: function () {
        this.number = this.generateNumber()
      },

      generateNumber: function () {
        return Math.floor(Math.random()*(this.max-this.min+1)+this.min);
      },

      // Is this really needed? 
      // handleSave() {
      //   console.log(this.number + ' was saved to local storage')
      // },

      handlePickAnotherNumber() {
        this.number = 0
        this.min = ''
        this.max = ''
      }
    },

    watch: {
      // number(newNumber) {
      //   localStorage.number = newNumber
      //   console.log(localStorage.number = newNumber)
      // }
    },
  }
</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Open+Sans|Roboto&display=swap');
@import url('https://fonts.googleapis.com/css?family=Bowlby+One+SC&display=swap');

h1, h3 {
  font-family: 'Bowlby One SC', cursive;
}
p {
  font-family: 'Roboto', sans-serif;
}
.margin-top15 {
  margin-top: 15px;
}
.margin-bottom15 {
  margin-bottom: 15px;
}
.margin-top20 {
  margin-top: 20px;
}
.margin-bottom20 {
  margin-bottom: 20px;
}
.margin-top40 {
  margin-top: 40px;
}
.margin-bottom40 {
  margin-bottom: 40px;
}
.logo {
  font-size: calc(35px + 0.8vw);
  font-weight: 400;
  text-shadow: 1px 1px 1px #000, 1px 1px 1px #3e3e3e;
  color: #fff;
  font-family: 'Bowlby One SC', cursive;
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
.randomNumberButton {
  margin: 0 auto;
  background: #21D4FD;
    background-color: #21D4FD;
    background-image: linear-gradient(19deg, #21D4FD 0%, #B721FF 100%);
}
.randomNumberButton>span {
  color: white;
  font-size: 1.22em;
  font-weight: bold;
}
.random-quote {
  margin: 20px 0;
  width: 75%;
  text-align: center;
  display: inline-block;
  color: #fff;
}
</style>