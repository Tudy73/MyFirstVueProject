<script setup>
import {ref} from "vue";

const response = ref('');
const firstName = ref('');
const lastName = ref('');
const address = ref('');
const termsOfService = ref(false);
const gender = ref('Man');
const city = ref('');

const emit = defineEmits(['next-page','increment']);
const props = defineProps({
  commonInfo: Number
})

function requiredFields(){
  return termsOfService.value && firstName.value
      && lastName.value && city.value;
}

function onSubmit() {
  if(requiredFields()){
    // response.value = `Hello ${(gender.value === "Man")?"Sir":"Miss"}
    // ${firstName.value} ${lastName.value}!!!
    // ${address.value?("You live at the address " + address.value):''}`
    // firstName.value = '';
    // lastName.value = '';
    // address.value = '';
    emit('next-page');
  }
  else{
    response.value = 'Please complete the required fields';
  }
}
</script>

<template>

  <div>
    <button @click="$emit('increment')">The shared number: {{props.commonInfo}}</button>
    <br>
    <span>FirstName:</span>
    <input v-model="firstName" placeholder="enter first name">
    <span v-if="!firstName" style="color: red">This field is required</span>
    <br>
    <span>LastName:</span>
    <input v-model="lastName" placeholder="enter last name">
    <span v-if="!lastName" style="color: red">This field is required</span>
  </div>
  <div>
    <span>Address:</span>
    <textarea v-model="address" placeholder="enter your address"></textarea>
  </div>
  <div>
    <span>Gender:</span>
    <input type="radio" id="man" v-model="gender" value="Man">
    <label for="man">Man</label>
    <input type="radio" id="woman" v-model="gender" value="Woman">
    <label for="woman">Woman</label>
    <br>
    <select v-model="city" id="city">
      <option disabled value="">Please select one</option>
      <option>Cluj</option>
      <option>Bucuresti</option>
      <option>Timisoara</option>
      <option>Iasi</option>
      <option>Constanta</option>
    </select>
    <label for="city">Your city</label>
  </div>
  <div>
    <input type="checkbox" v-model="termsOfService">
    <span>Accept the Terms of Service</span>
    <span v-if="!termsOfService " style="color: red">This field is required</span>
    <br>
    <button @click="onSubmit">
      Next
    </button>
    <br>
    <span>
        {{ response }}
    </span>
  </div>

</template>

<style scoped>
.required.text-content::after {
  content: " This field is required";
}
</style>