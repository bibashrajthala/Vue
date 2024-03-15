<template>
  <!-- EVENT HANDLING =>  x-on:<event-name> -->
  <h2>{{ name }}</h2>
  <button v-on:click="name = 'Rachit'">change name</button>

  <h2>{{ count }}</h2>
  <button v-on:click="incrementByOne">Increase by one</button>
  <button v-on:click="decrementByOne">Decrease by one</button>
  <button v-on:click="increment(5)">Increase by 5</button>
  <button v-on:click="decrement(5)">Decrease by 5</button>

  <!-- shorthand syntax for x-on  -->
  <!-- event is passed to method by defualt if no argument is provided -->
  <h2>{{ name }}</h2>
  <button @click="changeName">change name</button>

  <!-- in case args is needed to be passed , passing event as $event is required to use event in method -->
  <button v-on:click="decrement(5, $event)">Decrease by 5</button>

  <!-- can use multiple methods in single event using commma, but while chaining methods , you need to pass $event , as it wont be passed event though no arg is passed in method -->
  <button v-on:click="changeName($event), decrement(5, $event)">
    Decrease by 5 and change name
  </button>

  <!-- FORM HANDLING => v-model  -->
  <!-- to sync form data residing in script part and form controls residing in template part , we use v-model . this assures 2 way binding ie transfer form values from template to form data of script while adding data and also while editing to provided data to edit from script to template -->

  <!-- display form data  -->
  <div>
    {{ JSON.stringify(formValues, null, 2) }}
  </div>

  <form @submit="handleSubmit">
    <!-- text input  -->
    <div>
      <label for="name">Name</label>
      <input type="text" id="name" v-model="formValues.name" />
    </div>

    <!-- text area  -->
    <div>
      <label for="about">About</label>
      <textarea id="about" v-model="formValues.about" />
    </div>

    <!-- select  -->
    <div>
      <label for="country">Country</label>
      <select id="country" v-model="formValues.country">
        <option value="">Select a country</option>
        <option value="india">india</option>
        <option value="nepal">nepal</option>
        <option value="china">china</option>
      </select>
    </div>

    <!-- multiple select  -->
    <div>
      <label for="states">Country</label>
      <select multiple id="states" v-model="formValues.states">
        <option value="ktm">ktm</option>
        <option value="bkt">bkt</option>
        <option value="llt">llt</option>
      </select>
    </div>

    <!-- single checkbox  -->
    <div>
      <label for="rememberMe">remember me</label>
      <input type="checkbox" id="rememberMe" v-model="formValues.rememberMe" />
    </div>

    <!-- single checkbox with boolean value change to different value  -->
    <div>
      <label for="remoteWork">Open to remote work</label>
      <input type="checkbox" id="remoteWork" v-model="formValues.remoteWork" true-value="yes" false-value="no"/>
    </div>

    <!-- multiple checkbox  -->
    <!-- radio  -->
    <div>
      <label for="gender">html</label>
      <input type="checkbox" id="html" value="html" v-model="formValues.skills" />
      <label for="css">css</label>
      <input type="checkbox" id="css" value="css" v-model="formValues.skills" />
      <label for="js">js</label>
      <input type="checkbox" id="js"  value="js" v-model="formValues.skills" />
    </div>

    <!-- radio  -->
    <div>
      <input type="radio" id="male"  value="male" v-model="formValues.gender" />
      <label for="male">Male</label>
      <input type="radio" id="female"  value="female" v-model="formValues.gender" />
      <label for="female">Female</label>
      <input type="radio" id="others"  value="others" v-model="formValues.gender" />
      <label for="others">Others</label>
    </div>

    <button>submit</button>
  </form>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      name: "bibash",
      count: 0,

      formValues: {
        name: "",
        about: "",
        country: "",
        states: [],
        rememberMe: false,
        remoteWork: "no",
        skills:[],
        gender: "",
      },
    };
  },

  methods: {
    incrementByOne() {
      return this.count++;
    },
    decrementByOne() {
      return this.count--;
    },
    increment(num) {
      return (this.count = this.count + num);
    },
    decrement(num, event) {
      console.log("event in decrement", event);

      return (this.count -= num);
    },

    changeName(event) {
      console.log("event in change name", event);
      this.name = "Rachit";
    },

    handleSubmit(event){
      event.preventDefault()
      console.log("form data",this.formValues)
    }
  },
};
</script>

<style></style>
