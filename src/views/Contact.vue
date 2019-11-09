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
            <div class="contact">
                <h2>Contact Me Page</h2>
                <a href="https://twitter.com/carltonstith" target="_blank">
                <v-btn class="mx-2" fab dark large color="purple">
                    <i class="fab fa-twitter"></i>
                </v-btn>
                </a>
                <!-- <v-btn class="mx-2" fab dark large color="purple">
                    <i class="fab fa-twitter"></i>
                </v-btn> -->
            </div>
  
          </v-col>
        </v-row>
      </v-container>
    </v-content>
    <v-footer
      app
      class="purple"
    >
      <span class="white--text">&copy; 2019 Carlton Stith for CeeJayS Media</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
    name: 'Contact',
    data: () => ({
      drawer: null
    })
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
a {
    text-decoration: none;
}
.logo {
  font-size:calc(20px + 0.8vw);
}
.fab.fa-twitter {
    font-size: 1.8em;
}

</style>