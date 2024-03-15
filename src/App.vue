<template>
  <!-- modifiers  -->
  <!-- commonly used modifiers :number, prevent, lazy, trim, <keyboard-button-name>, etc  -->
  <!-- display form data  -->
  <div>
    {{ JSON.stringify(formValues, null, 2) }}
  </div>

  <form @submit.prevent="handleSubmit">
    <!-- text input  -->
    <div>
      <label for="name">Name</label>
      <input type="text" id="name" v-model.trim.lazy="formValues.name" />
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
      <input
        type="checkbox"
        id="remoteWork"
        v-model="formValues.remoteWork"
        true-value="yes"
        false-value="no"
      />
    </div>

    <!-- multiple checkbox  -->
    <!-- radio  -->
    <div>
      <label for="gender">html</label>
      <input
        type="checkbox"
        id="html"
        value="html"
        v-model="formValues.skills"
      />
      <label for="css">css</label>
      <input type="checkbox" id="css" value="css" v-model="formValues.skills" />
      <label for="js">js</label>
      <input type="checkbox" id="js" value="js" v-model="formValues.skills" />
    </div>

    <!-- radio  -->
    <div>
      <input type="radio" id="male" value="male" v-model="formValues.gender" />
      <label for="male">Male</label>
      <input
        type="radio"
        id="female"
        value="female"
        v-model="formValues.gender"
      />
      <label for="female">Female</label>
      <input
        type="radio"
        id="others"
        value="others"
        v-model="formValues.gender"
      />
      <label for="others">Others</label>
    </div>

    <!-- text input  -->
    <div>
      <label for="age">age</label>
      <input @keyup.enter="handleSubmit" type="number" id="age" v-model.number="formValues.age" />
      <!-- <input @mouseleave="handleSubmit" type="number" id="age" v-model.number="formValues.age" /> -->
    </div>

    <button>submit</button>
  </form>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      formValues: {
        name: "",
        about: "",
        country: "",
        states: [],
        rememberMe: false,
        remoteWork: "no",
        skills: [],
        gender: "",
        age:null
      },
    };
  },

  methods: {
    handleSubmit() {
      console.log("form data", this.formValues);
    },
  },
};
</script>

<style></style>
