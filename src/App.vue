<template>
  <section class="container">
    <FormComponent @form-submit="handleFormSubmit"/>
    <ResultComponent :formData="data"/>
  </section>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import FormComponent from './components/FormComponent.vue';
import ResultComponent from './components/ResultComponent.vue';
import { IFormData } from './interfaces/IFormData';


export default defineComponent({
  name: 'App',
  components: {
    FormComponent,
    ResultComponent
},
emits: ['form-submit'],
setup() {
  let data = ref({})
  const handleFormSubmit = (formData: IFormData) => {
    data.value = formData
  } 





  return {
    handleFormSubmit,
    data
  }
}

});
</script>

<style lang="scss">
@import "styles/variables";

* {
  margin: 0;
  padding: 0;
}


#app {
  display: flex;
  width: 100vw;
  height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: $Light-grey;

}

.container {
  margin: auto;
  justify-content: center;
  align-items: center;
  background-color: $White;
  width: 600px;
  border-radius: 1rem 1rem 10rem .1rem;

  input[type=number]::-webkit-inner-spin-button {
    -webkit-appearance: none;
  }

  input[type=number] {
    -moz-appearance: textfield;
    appearance: textfield;
  }
}
</style>
