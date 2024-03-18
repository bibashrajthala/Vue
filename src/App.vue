<template>
  <!-- PROPS  -->

  <!-- static props  -->
  <Greet name="Bibash" heroName="Bish" />
  <!-- dynamic props with v-bind  -->
  <Greet :name="name" :heroName="heroName" />
  <!-- some prefer kabab-case in html and camelCase in js , and vue know how to transform kebabcase html to camelcase prop, but for consistency only use one of the casing way  -->
  <Greet :name="name" :hero-name="heroName" />

  <!-- PROP TYPES AND VALIDATIONS  -->
  <!-- make age and isPublished dynamic props to make it accept other values, otherwise it takes that as string -->
  <!-- for non prop (pre existing) attributes like id, style, class, type, placeholder, etc , by defualt it gets set to root element of component, if it dont have single root component, it dont gets applied to any component, but this can be changed using inheritAttrs=true or false to say if root component should use it, and binding $attrs to element to want to set attributes  -->
  <Article  title="Article Title" :age="20" :isPublished="true" id="my-article" />



</template>

<script>
import Greet from "./components/Greet.vue";
import Article from "./components/Article.vue";

export default {
  name: "App",
  components: {
    Greet,
    Article,
  },
  data() {
    return {
      name: "Bibash",
      heroName: "Bish",
    };
  },
};
</script>

<style></style>
