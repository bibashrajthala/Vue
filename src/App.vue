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

    Ref
    <h3>{{ c_firstName }}</h3>
    <h3>{{ c_lastName }}</h3>
    <h3>{{ greet_julia }}</h3>

    <h3>{{ o_firstName }}</h3>

    Reactive
    <h3>{{ reactiveName.fname }} {{ reactiveName.lname }}</h3>

    test
    <h4>{{ testName }}</h4>
    <button @click="testName = 'test3'">change test name</button>

    test reactive
    <h4>{{ test }}</h4>

    methods in composition
    <button @click="chnageNameRef">change ref name</button>
    <button @click="chnageNameReactive">change reactive name</button>
  </div>

  computed
  <h3>Ref full name {{ fullnameRef }}</h3>
  <h3>Ref full name {{ fullnameReactive }}</h3>

  v-model
  <div>
    <!-- v-model with ref  -->
    <input type="text" v-model="city" />

    <!-- v-model with reactive  -->
    <input type="text" v-model="state" />
    <input type="text" v-model="province" />
  </div>

  watchers
  <div></div>
</template>

<script>
import { reactive, ref, toRefs, computed, watch } from "vue";

export default {
  name: "App",
  setup() {
    const c_firstName = ref("mark");
    c_firstName.value = "Julia";
    const greet = `hello ${c_firstName.value}`;

    const reactiveName = reactive({
      fname: "hello",
      lname: "world",
    });

    let testName = "test";
    testName = "test2";

    const testReactive = reactive({
      test: "helllo",
    });

    //methods
    function chnageNameRef() {
      c_firstName.value = "changed Firstname ref";
    }

    function chnageNameReactive() {
      reactiveName.fname = "changed Firstname reactive";
    }

    // computed
    const fullnameRef = computed(function () {
      return `${c_firstName.value}`;
    });

    const fullnameReactive = computed(function () {
      return `${reactiveName.fname} ${reactiveName.lname}`;
    });

    // for v-model

    const city = ref("");

    const location = reactive({
      state: "",
      province: "bagmati",
    });

    // watchers
    // for ref
    watch(city, function (newcity, oldcity) {
      console.log("watch ref new", newcity);
      console.log("watch ref old", oldcity);
    });

    // for reactive
    watch(location, function (newlocation, oldlocation) {
      console.log("watch reawctive new", newlocation);
      console.log("watch reactive old", oldlocation);
    });

    // watch multiple state data
    watch([city, location], function (newValue, oldValue) {
      console.log("watch combined new", newValue); //array
      console.log("watch combined old", oldValue); //array
      console.log("watch new city from combined ", newValue[0]);
      console.log(
        "watch new location's state from combined ",
        newValue[1].state
      );
    });

    return {
      c_firstName,
      greet_julia: greet,
      c_lastName: ref("wayne"),
      reactiveName,
      testName,
      ...toRefs(testReactive),
      chnageNameRef,
      chnageNameReactive,
      fullnameRef,
      fullnameReactive,
      city,
      ...toRefs(location),
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
