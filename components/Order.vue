<template>
    <div>
        <template  v-for="(clothe, index) of (clothes)" >
        <template>
        <v-subheader
           :key="clothe.id"
        ></v-subheader>

        <v-divider
           :key="index"
        ></v-divider>

        <v-list-item
         :key="clothe.name"
        >
          <v-list-item-avatar>
            <v-img :src="require('@/static/product-icon.jpg')"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-html="'Название: ' + clothe.name"></v-list-item-title>
            <v-list-item-subtitle v-html="'Артикул: ' + clothe.article"></v-list-item-subtitle>
            <v-list-item-subtitle v-html="'Цена: ' + clothe.price"></v-list-item-subtitle>
            <v-list-item-subtitle v-html="'Осталось штук: ' + clothe.amount"></v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
        </template>
      </template>
    </div>
</template>

<script>
export default {
    props: ['clothes'],
    name: 'Order'
}
</script>
