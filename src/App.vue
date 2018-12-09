<template>
  <v-app id="inspire" dark>
    <v-navigation-drawer
      v-model="drawer"
      clipped
      fixed
      app
    >
      <v-list dense>
        <v-list-tile @click="">
          <v-list-tile-action>
            <i class="fas fa-archway"></i>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>메뉴1</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile @click="">
          <v-list-tile-action>
            <i class="fas fa-archway"></i>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>메뉴2</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar app fixed clipped-left>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title>Vue 프로그램 연습</v-toolbar-title>
    </v-toolbar>
    <v-content>
      <Test/>
      <!-- <v-container fluid fill-height>
        <v-layout justify-center align-center>
          <v-flex shrink>
            <v-tooltip right>
              <v-btn
                slot="activator"
                :href="source"
                icon
                large
                target="_blank"
              >
                <v-icon large>code</v-icon>
              </v-btn>
              <span>Source</span>
            </v-tooltip>
            <v-tooltip right>
              <v-btn slot="activator" icon large href="https://codepen.io/johnjleider/pen/qxQWda" target="_blank">
                <v-icon large>mdi-codepen</v-icon>
              </v-btn>
              <span>Codepen</span>
            </v-tooltip>
          </v-flex>
        </v-layout>
      </v-container> -->
    </v-content>
    <v-footer app fixed>
      <span>&copy; 2018 / 12 / 09</span>
    </v-footer>
  </v-app>
</template>

<script>
  import Test from './cpnt/test/Test'
  export default {
    components: {
      Test
    },
    data: () => ({
      drawer: null
    }),
    props: {
      source: String
    }
  }
</script>