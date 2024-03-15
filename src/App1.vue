<!-- binding data  -->

<template>
  <!-- text interpolation with moustache syntax -->
  <div>{{ greet }} {{ name }}</div>

  <!-- binding text data with v-text directive as inner text .This completely overrides the existing inner text  -->
  <div v-text="fullname"></div>

  <!-- binding html  -->
  <!-- will display html as text  -->
  <div v-text="boldName"></div>
  <div>{{ boldName }}</div>

  <!-- will display as html  -->
  <div v-html="boldName"></div>

  <div v-html="hack"></div>

  <!-- binding attributes  -->
  <div v-bind:id="headingId">this is heading</div>
  <button v-bind:disabled="isDisabled">button</button>

  <!-- bind multiple attributes at once using object  -->
  <button v-bind="multipleAttributes">button with id button2 disabled</button>

  <!-- binding class and styles -->

  <!-- binding class  -->
  <!-- static class  -->
  <h2 class="underlined">underlined text</h2>

  <!-- dynamic class  -->
  <h2 v-bind:class="status">status</h2>

  <!-- static + dynamic class  -->
  <h2 class="underlined" v-bind:class="status">underlined status</h2>

  <!-- conditional class  -->
  <h3 v-bind:class="isPromoted && 'promoted'">promoted ?</h3>
  <h3 v-bind:class="isSoldOut ? 'sold-out' : 'new'">sold out ?</h3>

  <!-- multiple dynamic classes with array or object  -->
  <h3 v-bind:class="['promoted', 'sold-out']">Multiple array classes</h3>
  <h3 v-bind:class="[isPromoted && 'promoted', isSoldOut ? 'sold-out' : 'new']">
    Multiple array classes with conditonals
  </h3>
  <h3
    v-bind:class="{
      promoted: isPromoted,
      'sold-out': isSoldOut,
      new: !isSoldOut,
    }"
  >
    Multiple object classes with conditonals
  </h3>

  <!-- binding inline styles  -->
  <h3
    v-bind:style="{
      padding: '20px', // static
      color: highlightColor, // dynamic
      fontSize: headerSize + 'px',
      // or, // 'font-size':headerSize + 'px'
    }"
  >
    Inline styles
  </h3>

  <h3 v-bind:style="headerStyleObject">Inline styles With an dynamic object</h3>

  <!-- object that comes later overrides styles from object coming before them in case of conflict  -->
  <h3 v-bind:style="[baseStyleObject, successStyleObject]">
    Multiple Inline styles object: Success
  </h3>
  <h3 v-bind:style="[baseStyleObject, dangerStyleObject]">
    Multiple Inline styles object: Danger
  </h3>

  <!-- shorthand of v-bind  -->
  <h3 :style="[baseStyleObject, dangerStyleObject]">
    Multiple Inline styles object: Danger
  </h3>
  <h3 :class="isSoldOut ? 'sold-out' : 'new'">sold out ?</h3>

  <!-- conditional rendering  -->

  <!-- conditional rendering with if/ else if/ else -->

  <!-- display number is zero or not  -->
  <h3 v-if="num === 0">Number is zero</h3>
  <h3 v-else>Number is not a zero</h3>

  <!-- display number is zero or positive or negative or Nan -->
  <h3 v-if="num === 0">Number is zero</h3>
  <h3 v-else-if="num > 0">Number is positive</h3>
  <h3 v-else-if="num < 0">Number is negative</h3>
  <h3 v-else>Not a number</h3>

  <!-- Creates extra div tag in dom -->
  <div v-if="display">
    <p>{{ num }} {{ name }}</p>
    <p>Creates extra div tag in dom</p>
  </div>

  <!-- doesnot create extra tag in dom -->
  <!-- similar to fragment in react js  -->
  <template v-if="display">
    <p>{{ num }} {{ name }}</p>
    <p>doesnot create extra div tag in dom</p>
  </template>

  <!-- conditional rendering v-show directive -->
  <div v-show="showContent">
    <p>{{ num }} {{ name }}</p>
    <p>show content with v-show</p>
  </div>

  <!-- difference with conditional rendering of v-show and v-if/else is v-show uses display:none css whereas v-if completly mounts/unmounts element -->
  <!-- better to use v-show for situations like toggling elements to show and hide , cause mounting and unmounting multiple times cost performance, but if condition is only being checked once can use v-if  -->
  <h5 v-show="showContent">V-show</h5>
  <h5 v-if="showContent">V-if</h5>

  <!-- list rendering  -->
  <h3 v-for="name in names" v-bind:key="name">{{ name }}</h3>
  <!-- with index -->
  <h3 v-for="(name, i) in names" :key="name">{{ i }} {{ name }}</h3>

  <h3 v-for="name in fullNames" :key="name.first">
    {{ name.first }} {{ name.last }}
  </h3>

  <!-- nesting of loop -->
  <div v-for="actor in actors" :key="actor.name">
    <h3>{+{ actor.name }}</h3>
    <div v-for="movie in actor.movies" :key="movie">
      {{ movie }}
    </div>
  </div>

  <!-- looping for object is also possible -->
  <!-- loops as array of (value, key, index) -->
  <h3 v-for="value in actorDetails" :key="value">
    {{ value }}
  </h3>

  <h3 v-for="(value, key, index) in actorDetails" :key="value">
    {{ index }} {{ key }} {{ value }}
  </h3>

  <!-- looping a block but with template so that div is not added to dom -->
  <template v-for="name in names" :key="name">
    <h3>{{ name }}</h3>
    <hr />
  </template>

  <!-- key attribute has same purpose as in react js Virtual dom  -->

  <!-- conditional rendering with looping  -->

  <!-- v-if is executed before v-for when used on same element so name dont exist in v-if here, so it is wrong  -->
  <!-- <h3 v-for="name in names" v-bind:key="name" v-if="name ==='ram'">{{ name }}</h3> -->

  <!-- Recommended Solution:Use computed properties( in later session) -->

  <!-- Other solution: Use <template></template> -->
  <template v-for="name in names" :key="name">
    <h3 v-if="name === 'ram'">{{ name }}</h3>
  </template>

  <!-- methods in vue  -->
  <!-- binds the properties of data object to methods so dont use arrow function as method because 'this' keyword in arrow function work differently -->
  <h4>{{ 4 + 5 + 6 }}</h4>
  <h4>{{ 4 + 4 + 4 }}</h4>

  <h4>ADD Method : {{ add() }}</h4>
  <h4>ADD Method : {{ addWithArguments(5,6,7) }}</h4>
  <h4>Binded value Method : {{ multipyBinded(5) }}</h4>
  <h4>Binded value Method : {{ multipyBinded(mutipleValue) }}</h4>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      greet: "Namaste",
      name: "ABC",
      fullname: "bibash rajthala",
      boldName: "<b>Bold</b>",
      hack: `<a href='' onclick="alert('you have been hacked')">Win a prize !</a>`,
      headingId: "heading",
      isDisabled: false,
      multipleAttributes: {
        id: "button2",
        disabled: true,
      },

      status: "danger",
      isPromoted: true,
      isSoldOut: false,

      highlightColor: "orange",
      headerSize: 50,
      headerStyleObject: {
        padding: "20px",
        fontSize: "50px",
        color: "orange",
      },

      baseStyleObject: {
        padding: "20px",
        fontSize: "18px",
      },
      dangerStyleObject: {
        padding: "10px",
        color: "red",
      },
      successStyleObject: {
        color: "green",
      },

      num: "hi",
      name: "ram",
      display: true,

      showContent: false,

      names: ["ram", "shyam", "hari"],
      fullNames: [
        { first: "ram", last: "shrestha" },
        { first: "shyam", last: "poudel" },
        { first: "hari", last: "raut" },
      ],
      actors: [
        { name: "Christian Bale", movies: ["Batman", "The machinist"] },
        { name: "Dicraprio", movies: ["revenant", "titanic"] },
      ],

      actorDetails: {
        name: "Margot Robbie",
        latest: "Barbie",
      },

      baseValue:10,
      mutipleValue:3

      //
    };
  },

  methods:{
    add(){
      return 4+3+1
    },
    addWithArguments(a,b,c){
      return a+b+c
    },
    multipyBinded(arg){

      // use this keyword to use binded vlaues within the object 
      return arg * this.baseValue;
    }
  }
};
</script>

<style>
.underlined,
.promoted {
  text-decoration: underline;
}

.danger,
.sold-out {
  color: red;
}

.success,
.new {
  color: green;
}
</style>
