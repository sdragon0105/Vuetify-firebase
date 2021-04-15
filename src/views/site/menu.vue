<template>
  <v-list>
    <v-list-group
      v-for="(item, i) in items"
      :key="i"
      v-model="item.active"
      :prepend-icon="item.icon"
      no-action
    >
      <template v-slot:activator>
        <v-list-item-content>
          <v-list-item-title v-text="item.title" />
        </v-list-item-content>
      </template>

      <v-list-item
        v-for="subItem in item.subItems"
        :key="subItem.title"
      >
        <v-list-item-content>
          <v-list-item-title v-text="subItem.title" />
        </v-list-item-content>
      </v-list-item>
    </v-list-group>
  </v-list>
</template>

<script>
export default {
  data: () => ({
    items: [
      {
        icon: 'mdi-home',
        active: true,
        subItems: [
          { title: 'Dashboard', to: '/' },
          { title: 'About', to: '/about' }
        ],
        title: 'Home',
      },
      {
        icon: 'mdi-silverware-fork-knife',
        subItems: [
          { title: 'Breakfast & brunch' },
          { title: 'New American' },
          { title: 'Sushi' },
        ],
        title: 'Dining',
      },
      {
        icon: 'mdi-school',
        subItems: [{ title: 'List Item' }],
        title: 'Education',
      }
    ],
  })
}
</script>
