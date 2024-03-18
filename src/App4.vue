<template>
  <!-- Computed properties  -->
  <!-- they are similar to methods but they are cached and the computed properties run only when the dependencies of that property changes. -->
  <!-- used for expensive operations  -->
  <!-- highly perfromant  -->

  <h2>{{ firstname }} {{ lastname }}</h2>
  <h2>{{ fullname }}</h2>

  <!-- renders on each render  -->
  <h3>
    Data property total :
    {{ items?.reduce((curr, item) => curr + item.price, 0) }}
  </h3>
  <h3>Get total Method : {{ getTotal() }}</h3>

  <!-- rerenders on only dependency change  -->
  <h3>Computed total : {{ total }}</h3>

  <!-- as we can see when dependency ( here items array changes both method and  computed property runs ) -->
  <button @click="items?.push({ id: 4, title: 'hello', price: 50 })">
    add item
  </button>
  <br />

  <!-- but when other data changes here country changes method runs but computed property wont  -->
  <input type="text" v-model="country" />

  <!-- CONDITIONAL RENDERING  -->
  <!-- Method 1. use template with v-for and then v-if (NOT RECOMMENDED)  -->
  <!-- Method 2. use computed property (RECOMMENDED) => cached  -->

  <!-- display expensive items (item with price above 100) using both above methods  -->

  <!-- method 1  -->
  <template v-for="item in items" :key="item.id">
    <p v-if="item.price > 100">{{ item.title }} {{ item.price }}</p>
  </template>

  <!-- method 2  -->
  <p v-for="item in expensiveItems" :key="item.id">
    {{ item.title }} {{ item.price }}
  </p>

  <!-- until now we just read value of computed property , but we may need to get and set it, for that we use computed getter and setter -->
  <!-- lets use it for fullname computed property  -->
  <button @click="changeFullName">Change full name</button>

  <!-- this wont work as setter  -->
  <button @click="fullname('Hello World')">Change full name 2</button>

  <!-- WATHCHERS  -->
  <!-- similar to computed properties , used to watch the value change in data or computed properties  -->
  <!-- create volume tracker 0 to 20 => when vol reach 16 show High volume warning -->

  <h3>Volume (0 - 20) : {{ volume }}</h3>
  <button @click="volume += 2">Add Volume</button>
  <button @click="volume -= 2">Substract Volume</button>

  watchers and computed properties can be used interchangebly but when to use
  which one:

  <img src="./assets/watchers/1.png" alt="1" width="100%" />
  <img src="./assets/watchers/2.png" alt="2" width="100%" />
  <img src="./assets/watchers/3.png" alt="3" width="100%" />
  <img src="./assets/watchers/4.png" alt="4" width="100%" />

  <!-- IMMEDIATE AND DEEP WATHERS  -->

  <!-- watcher movie is only called when change is detected in movie but what if we immediately want to call api inside movie watcher with inital value of movie when page loads? -->
  <input type="text" v-model="movie" />

  <!-- for that we use differnt object syntax for watcher with handler methods which receives same args and immediate property with it  -->
  <!-- now when you refresh the page you see movieImmediate watcher is called immediately  -->
  <input type="text" v-model="movieImmediate" />

  <!-- for nested data or computed properties ie objects and arrays, we need to use deep property with watcher if the data is mutated for watcher to run/detect the change in (deeply) nested property of object or array, but if different reference is retuned deep property is not needed, watcher can detect it 
   -->

  <!-- eg : Mutated  -->
  <!-- v-model syncs by mutating data  -->
  <input type="text" v-model="movieInfo.title" />
  <input type="text" v-model="movieInfo.actor" />
  <button @click="movieList.push('Wonder Woman')">Add movie</button>

  <!-- eg: not mutated  -->
  <button @click="movieList = [...movieList, 'Wonder Woman']">Add movie</button>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      firstname: "Bibash",
      lastname: "Rajthala",
      items: [
        { id: 1, title: "TV", price: 100 },
        { id: 2, title: "Mobile", price: 200 },
        { id: 3, title: "radio", price: 300 },
      ],
      country: "",
      volume: 0,
      movie: "",
      movieImmediate: "Batman",
      movieInfo:{
        title:"Batman",
        actor:"Bale"
      },
      movieList:['Batman', 'Superman']
    };
  },

  methods: {
    getTotal() {
      console.log("method");

      return this.items?.reduce((curr, item) => curr + item.price, 0);
    },
    changeFullName() {
      this.fullname = "Rachit Bhusal"; //goes to setter of fullname computed property
    },
  },
  computed: {
    // fullname() {
    //   return `${this.firstname} ${this.lastname}`;
    // },
    fullname: {
      get() {
        return `${this.firstname} ${this.lastname}`;
      },
      set(value) {
        const name = value?.split(" ");
        // set by syncing with data properties
        this.firstname = name[0];
        this.lastname = name[1];
      },
    },
    total() {
      console.log("computed");
      return this.items?.reduce((curr, item) => curr + item.price, 0);
    },
    expensiveItems() {
      return this.items.filter((item) => item.price > 100);
    },
  },
  watch: {
    // should have same name as data or computed property to watch the corresponding property
    // gives updated and prev value in arg
    volume(newValue, prevValue) {
      if (newValue === 16 && newValue > prevValue) alert("High Volume");
    },

    movie(newValue) {
      console.log(`Calling api with new movie value ${newValue}`);
    },
    movieImmediate: {
      handler(newValue) {
        console.log(`Calling api with new movie value ${newValue}`);
      },
      immediate:true
    },
    movieInfo: {
      handler(newValue) {
        console.log(`Calling api with new movie info ie title ${newValue.title} and actor ${newValue.actor} `);
      },
      deep:true
    },
    movieList: {
      handler(newValue) {
        console.log(`updated list: ${newValue}`);
      },
    //   deep:true
    },
  },
};
</script>

<style></style>
