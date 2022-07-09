<template>
  <div>
    <div class="pages">
      <v-btn v-on:click="sortNames">Отсортировать вещи по названию в алфавитном порядке</v-btn>
    </div>
    <v-btn v-if="!isFives" v-on:click="filterByPrice">Отобразить только вещи с ценой больше 10000</v-btn>
    <v-btn v-if="isFives" v-on:click="show">Отобразить все</v-btn>
    <ul>
      <Order v-bind:clothes="clothes"/>
    </ul>
    <div class="pages">
      <v-btn v-on:click="prev">Предыдущая</v-btn>
      <v-btn v-on:click="next">След страница</v-btn>
    </div>
    <v-btn v-on:click="drop">Сбросить сортировку и фильтр</v-btn>
  </div>
</template>

<script>
import Order from '@/components/Order'

export default {
  data() {
    return {
      isFives: false
    }
  },
  components: {Order},
  async fetch({store}) {
    if (!store.getters['api/clothes']) {
      await store.dispatch('api/fetch')
    }
  },
  computed: {
    clothes() {
      return this.$store.getters['api/clothes'];
    }
  },
  methods: {
    async show() {
      this.isFives = !this.isFives
      await this.$store.dispatch('api/fetch')
    },
    async filterByPrice() {
      this.isFives = !this.isFives
      await this.$store.dispatch('api/filterByPrice', this.$store.getters['api/clothes'])
    },
    async next() {
      const next = this.$store.getters['api/next'];
      if (next) {
        this.$store.dispatch('api/fetchNext', next);
      } else {
        alert('Следующей страницы нет')
      }
    },
    async prev() {
      const prev = this.$store.getters['api/prev'];
      if (prev) {
        this.$store.dispatch('api/fetchPrev', prev);
      } else {
        alert('Предыдущей страницы нет')
      }
    },
    async sortNames() {
      await this.$store.dispatch('api/fetchAll');
      const clothes = this.$store.getters['api/clothes'];
      await this.$store.dispatch('api/sortByNames', clothes);
    },
    async drop() {
      this.isFives = false
      await this.$store.dispatch('api/fetch')
    }
  }
}
</script>

<style>
.pages {
  margin-top: 20px;
  margin-bottom: 20px;
}
</style>
