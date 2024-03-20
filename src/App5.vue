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
  <Article
    title="Article Title"
    :age="20"
    :isPublished="true"
    id="my-article"
  />

  <!-- COMPONENT EVENTS / EMIT  -->
  <button @click="showPopUp = true">Open Popup</button>

  <PopUp v-show="showPopUp" @close="closePopUp" />

  <!-- V-MODEL IN CUSTOM COMPONENTS  -->
  <Input v-model="name" placeholder="Enter name" />

  <!-- SLOT PROPS => pass data from child to parent  -->
  <NameList v-slot:default="slotProps">{{ slotProps.firstName }}</NameList>
  <NameList v-slot:default="slotProps"
    >{{ slotProps.firstName }} {{ slotProps.lastName }}</NameList
  >
  <NameList>
    <template v-slot:slotWithFullName="slotProps">
      {{ slotProps.fullname.lastName }}
    </template>
  </NameList>

  <!-- COMPONENT STYLES  -->
  <!-- just like in react, styles are applied globally and since styles of child component are evalueated before parents, parent child overrides child styles on confilct. so use scope the styles or even better use module styles -->
  <!-- Also when root node is not provided inside template of child, it takes parent styles even when child styles are scoped
   -->
  <!-- And slots takes styles from parent component not form child  -->
  <h4>From parent</h4>
  <ChildStyles>
    <h4>From Slot</h4>
  </ChildStyles>

  <!-- DYNAMIC COMPONENTS  -->

  <button @click="activeTab = 'TabA'">Tab A</button>
  <button @click="activeTab = 'TabB'">Tab B</button>
  <button @click="activeTab = 'TabC'">Tab C</button>

  <!-- NOT RECOMMENDED : conventional method  -->
  <TabA v-if="activeTab === 'TabA'" />
  <TabB v-if="activeTab === 'TabB'" />
  <TabC v-if="activeTab === 'TabC'" />

  <!-- RECOMMENDED => use dynamic components  -->
  <!-- provide component name (given while importing) to is attribute using v-bind  -->
  <!-- in this case make sure component name is same as activeTab value  -->
  <component :is="activeTab" />

  <!-- caching the dynamic component -->
  <!-- dont create new instance of active component and dont rerender it  -->
  <keep-alive>
    <component :is="activeTab" />
  </keep-alive>

  <!-- TELEPORT  -->
  <!-- can teleport => define element or component in one place and display it in another even outside of vue root element #app of index.html of public folder  -->
  <!-- give element inside which you want it to teleport to , can use any css selector , id is the best one  -->
  <!-- even though its teleported it still propagates event to ancestors jus like normal vue dom elements => event bubbling/ evnt propagation -->
  <!-- usually use to create modal , drawer, tooltip etc -->
  <teleport to="#portal-root">
    <div>This component is teleported</div>
  </teleport>
</template>

<script>
import Greet from "./components/Greet.vue";
import Article from "./components/Article.vue";
import PopUp from "./components/PopUp.vue";
import Input from "./components/Input.vue";
import NameList from "./components/NameList.vue";
import ChildStyles from "./components/ChildStyles.vue";

import TabA from "./components/tabs/TabA.vue";
import TabB from "./components/tabs/TabB.vue";
import TabC from "./components/tabs/TabC.vue";

export default {
  name: "App",
  components: {
    Greet,
    Article,
    PopUp,
    Input,
    NameList,
    ChildStyles,
    TabA,
    TabB,
    TabC,
  },
  data() {
    return {
      name: "Bibash",
      heroName: "Bish",
      showPopUp: false,
      activeTab: "TabA",
    };
  },
  methods: {
    closePopUp(name) {
      console.log("data", name);
      this.showPopUp = false;
    },
  },
};
</script>

<style scoped>
h4 {
  color: red;
}
</style>
