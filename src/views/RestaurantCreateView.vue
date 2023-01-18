<template>
  <createRestaurant/>
</template>

<script>
import { defineComponent } from 'vue';

// Components
import createRestaurant from '../components/createRestaurant.vue';

export default defineComponent({
  name: 'RestaurantCreateView',
  components: {
    createRestaurant
  },
});
</script>
