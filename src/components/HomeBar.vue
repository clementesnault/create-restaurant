<template>
    <v-app-bar color="primary" elevation='4' prominent>
        <v-toolbar-title>{{ title }}</v-toolbar-title>
        <v-btn flat v-for="item in menuItems" :key ="item.title" :to="item.path">
        <v-icon left dark>mdi-{{ item.icon }}</v-icon>{{ item.title }}</v-btn>
    </v-app-bar>
</template>

<script>
    export default {
        data() {
            return{
                title: "Ubeuhreats",
                menuItems:[
                {title:"Home", path:"/", icon:"home"},
                {title:"Basket", path:"/basket", icon:"basket"},
              ]
            }
        }
    }
</script>