<template>
  <!-- COMPOSITION API
    -> makes code/logics encapsulated a/c to feature 
    eg: in options api, one file can have (data(for feature 1 and 2), methoods(for feature 1 and 2), computed(for feature 1 and 2), lifecycle methods(for feature 1 and 2),watchers(for feature 1 and 2) ) etc for feature 1 and 2 , while in composition api we can compose code/logics separately for feature 1 and feature 2 and so on.
    -> increases reusesability  -->
  <div>Composition api</div>

  <!-- COMPOSITION API VS OPTIONS API  -->
  <!-- ref vs data  -->
  <div>
    <!-- no need to use .value  for binding in template as vue does that for us , but in js part we need to use .value to react/mutate/access the value  -->
    <h3>{{ c_firstName }}</h3>
    <h3>{{ c_lastName }}</h3>
    <h3>{{ greet_julia }}</h3>

    <h3>{{ o_firstName }}</h3>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "App",
  setup() {
    const c_firstName = ref("mark");
    c_firstName.value = "Julia";
    const greet = `hello ${c_firstName.value}`;
    return {
      c_firstName,
      greet_julia: greet,
      c_lastName: ref("wayne"),
    };
  },
  data() {
    return {
      o_firstName: "Bruce",
    };
  },
};
</script>

<style scoped></style>
