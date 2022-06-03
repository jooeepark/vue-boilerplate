<template>
  <div class="login">
    <h1>{{ title }}</h1>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useRoute } from "vue-router";
export default defineComponent({
  setup() {
    const route = useRoute();

    return {
      title: route.meta.title,
    };
  },
});
</script>
