<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <site-title :title="title" />
      <v-spacer />

      <v-btn
        icon
        @click="save"
      >
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
      <v-btn
        icon
        @click="read"
      >
        <v-icon>mdi-check</v-icon>
      </v-btn>
      <v-btn
        icon
        @click="readOne"
      >
        <v-icon>mdi-check</v-icon>
      </v-btn>
      <v-menu
        left
        bottom
      >
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            icon
            v-bind="attrs"
            v-on="on"
          >
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

        <v-list>
          <v-list-item
            v-for="n in 5"
            :key="n"
            @click="() => {}"
          >
            <v-list-item-title>Option {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>

    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6">
            Application
          </v-list-item-title>
          <v-list-item-subtitle>
            subtext
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <v-divider />
      <site-menu />
    </v-navigation-drawer>

    <v-main>
      <router-view />
    </v-main>

    <site-footer
      :footer="footer"
    />
  </v-app>
</template>

<script>
import SiteTitle from '@/views/site/title'
import SiteFooter from '@/views/site/footer'
import SiteMenu from '@/views/site/menu'

export default {
  name: 'App',
  components: { SiteTitle, SiteFooter, SiteMenu },
  data () {
    return {
      drawer: false,
      title: "Main Page",
      footer: "@main.com"
    }
  },
  mounted () {
    console.log(this.$firebase)
  },
  methods: {
    save () {
      console.log('save@@@')
      this.$firebase.database().ref().child('abcd').set({
        title: 'abcd', text: 'ttttt'
      })
    },
    read () {
      this.$firebase.database().ref().child('abcd').on('value', (sn)=>{
        console.log(sn)
        console.log(sn.val())
      })
    },
    async readOne () {
      const sn = await this.$firebase.database().ref().child('abcd').once('value')
      console.log(sn.val())

    }
  }
}
</script>
