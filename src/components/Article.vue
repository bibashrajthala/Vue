<template>
  <div>
    Ariticle component


    <!-- set non props attributes passed from parent component to this element m -->
    <h2 v-bind="$attrs">{{ title }}</h2>

    <h3>Age: {{ age }}</h3>

    <h4>Published: {{ isPublished ? "Yes" : "No" }}</h4>

    <!-- PROVIDE / INJECT  -->
    <!-- just like context api in react js => avoid prop drilling  -->
 <!-- directly use provide as object to provide to all child components if you dont need to use that data in providing parent component else use data property then bind data to provide object  -->
    <PartOfAritcle/>

    <!-- this is same section name from parent  -->
    <h4>From providing compoennt -{{partName}}</h4>
  </div>
</template>

<script>
import PartOfAritcle from './PartOfAritcle.vue';

export default {
  name: "Article",
  components:{PartOfAritcle},

  data(){
    return {
        partName:"Story"
    }

  },
  provide(){
    return {
        sectionName:this.partName
    }
  },

//   provide:{
//     sectionName:'Story'
//   },
  props: {
    title: {
      type: String,
      required: true,
      default: "Article Default title",
    },
    age: Number,
    isPublished: Boolean,
    commentIds: Array,
    author: Object,
    callback: Function,
    contactsPromise: Promise, // or any other constructor
  },
  inheritAttrs:false
};
</script>

<style></style>
