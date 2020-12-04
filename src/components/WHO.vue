<template>
  <v-app>
    <v-app-bar app clipped-left>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>
        COVID-19
        <span v-show="$vuetify.breakpoint.smAndUp">Dashboard</span>
      </v-toolbar-title>

      <v-spacer></v-spacer>
      <v-btn text value="left" @click="home">
        <v-icon left>mdi-home-variant-outline</v-icon>
        <span class="hidden-sm-and-down">Home</span>
      </v-btn>

      <v-btn text value="right" @click="chart">
        <!-- chart-bell-curve-cumulative -->
        <v-icon left>mdi-chart-areaspline</v-icon>
        <span class="hidden-sm-and-down">Global</span>
      </v-btn>
      <!-- <v-btn text value="right" @click="Ranking">
        chart-bell-curve-cumulative
        <v-icon left>mdi-chart-bar</v-icon>
        <span class="hidden-sm-and-down">Ranking</span>
      </v-btn> -->
      <v-btn text value="right" @click="who">
        <!-- chart-bell-curve-cumulative -->
        <v-icon left>mdi-hospital-box</v-icon>
        <span class="hidden-sm-and-down">About COVID19</span>
      </v-btn>

      <v-tooltip bottom :dark="isDarkTheme">
        <!-- <template v-slot:activator="{ on }">
          <v-btn icon v-on="on" @click="TOGGLE_THEME">
            <v-icon>mdi-theme-light-dark</v-icon>
          </v-btn>
        </template>
        <span>风格切换</span> -->
      </v-tooltip>
    </v-app-bar>
    <v-content>
      <iframe
        src="https://www.who.int/emergencies/diseases/novel-coronavirus-2019/advice-for-public"
        style="width: 100%;height:100%;"
        frameborder="0"
        id="Chart"
      ></iframe>
    </v-content>
  </v-app>
</template>

<script>
import { mapState, mapMutations } from 'vuex';

export default {
  name: 'WHO',
  computed: {
    ...mapState(['isDarkTheme'])
  },
  watch: {
    isDarkTheme(val) {
      this.$vuetify.theme.dark = val;
      // this.checkTheme();
    }
  },
  methods: {
    ...mapMutations(['TOGGLE_THEME']),

    chart() {
      this.$router.replace('/Chart');
    },
    home() {
      this.$router.replace('/');
    },
    who() {
      this.$router.replace('/WHO');
    },
    Ranking() {
      this.$router.replace('/Ranking');
    },
    checkTheme() {
      // console.log('mm', this.$vuetify.theme.dark);
      if (this.$vuetify.theme.dark) {
        document
          .getElementById('Chart')
          .contentWindow.document.getElementByTag('ChartBody')
          .setAttribute('style', 'background-color: black;');
      } else {
        document
          .getElementById('Chart')
          .contentWindow.document.getElementById('ChartBody')
          .setAttribute('style', 'background-color: white;');
      }
    }
  }
};
</script>
