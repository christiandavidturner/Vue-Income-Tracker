<template>
  <!-- <form v-on="submit"> -->
  <form @submit.prevent="FormHandler">
    <input type="text" placeholder="Description" v-model="formData.desc" />
    <input type="number" placeholder="Amount" v-model="formData.value" />
    <input type="date" placeholder="Date" v-model="formData.date" />
    <input type="submit" value="Submit" />
  </form>
</template>

<script>
import { reactive } from "vue";

export default {
  props: {
    state: Object,
  },
  // we'll get props down from parent
  // A) emit allows us to pass events back up to parent
  setup(props, { emit }) {
    const formData = reactive({
      desc: null,
      value: null,
      date: null,
    });

    function FormHandler() {
      // console.log(formData);

      // B) the second parameter, the object, is what we'll pass back up to our App component
      emit("add-income", {
        desc: formData.desc,
        value: formData.value,
        date: formData.date,
      });

      formData.desc = null;
      formData.value = null;
      formData.date = null;
    }

    return {
      FormHandler,
      formData,
    };
  },
};
</script>

<style scoped>
form {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}
form input {
  color: #888;
  border: none;
  outline: none;
  font-size: 20px;
}
form input::placeholder {
  color: #aaa;
}
form input:not([type="submit"]) {
  display: block;
  background: #fff;
  border: none;
  outline: none;
  padding: 5px 15px;
}
form input[type="submit"] {
  display: block;
  background: none;
  border: none;
  outline: none;
  color: #fff;
  font-weight: 500;
  text-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  padding: 5px 15px;
  background-color: #ffce00;
  cursor: pointer;
}
form input:first-of-type {
  border-radius: 8px 0px 0px 8px;
}
form input:last-of-type {
  border-radius: 0px 8px 8px 0px;
}
</style>
