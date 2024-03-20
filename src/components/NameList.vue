<template>
  <h3 v-for="name in names" :key="name.firstName">
    <slot :firstName="name.firstName" :lastName="name.lastName"></slot>
    <slot name="slotWithFullName" :fullname="name"></slot>
  </h3>
</template>

<script>
export default {
  name: "NameList",
  data() {
    return {
      names: [
        {
          firstName: "Bruce",
          lastName: "Wayne",
        },
        {
          firstName: "Kent",
          lastName: "Clark",
        },
      ],
    };
  },
};
</script>

<style></style>
