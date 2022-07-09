<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :clipped="clipped"
      :mini-variant="miniVariant"
      app
      fixed
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          exact
          router
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title"/>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" app fixed>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"/>

      <v-toolbar-title v-text="title"/>
      <v-spacer/>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt/>
      </v-container>
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<style scoped>
.left_widget {
  padding: 10px;
}
</style>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-apps",
          title: "Главная",
          to: "/",
        },
        {
          icon: "mdi-chart-bubble",
          title: "О нас",
          to: "/about",
        },
        {
          icon: "mdi-antenna",
          title: "Одежда",
          to: "/clothes",
        },
        {
          icon: "mdi-plus",
          title: "Добавить пользователя",
          to: "/create",
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: "Магазин одежды",
    };
  },
};
</script>
