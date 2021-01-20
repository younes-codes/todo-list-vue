<template>
  <div class="home">
    <todos></todos>
  </div>
</template>

<script>
import todos from "./todos";
// @ is an alias to /src
export default {
  components: {
    todos,
  },
};
</script>
