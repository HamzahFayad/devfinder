<template>
  <div>
    {{ userBio }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      props: ["user"],
      userBio: "",
    };
  },
  methods: {},
};
</script>

<style lang="scss">
</style>