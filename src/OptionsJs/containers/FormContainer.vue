<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <TextInput
        label="CEP"
        identifier="cep"
        v-model="zipCodeInput"
        @input="checkLength"
        :maxLength="8"
      />
      <TextInput label="Logradouro" identifier="street" v-model="streetInput" />
      <TextInput
        label="Bairro"
        identifier="neighborhood"
        v-model="neighborhoodInput"
      />
      <TextInput label="Cidade" identifier="city" v-model="cityInput" />
      <TextInput label="Estado" identifier="state" v-model="stateInput" />
      <button type="submit">Adicionar novo endereço</button>
    </form>
  </div>
</template>

<script>
import TextInput from "../components/TextInput.vue";
export default {
  name: "FormContainer",
  components: {
    TextInput,
  },
  data() {
    return {
      zipCodeInput: "",
      streetInput: "",
      neighborhoodInput: "",
      cityInput: "",
      stateInput: "",
    };
  },
  methods: {
    checkLength() {
      if (this.zipCodeInput.length === 8) this.fetchCep();
    },
    resetFields() {
      this.zipCodeInput = "";
      this.streetInput = "";
      this.neighborhoodInput = "";
      this.cityInput = "";
      this.stateInput = "";
    },
    async fetchCep() {
      const response = await fetch(
        `https://viacep.com.br/ws/${this.zipCodeInput}/json/`
      );
      const data = await response.json();
      const { logradouro, bairro, localidade, uf } = data;
      if (logradouro) this.streetInput = logradouro;
      if (bairro) this.neighborhoodInput = bairro;
      if (localidade) this.cityInput = localidade;
      if (uf) this.stateInput = uf;
    },
    handleSubmit() {
      const payload = {
        zipCode: this.zipCodeInput,
        street: this.streetInput,
        neighborhood: this.neighborhoodInput,
        city: this.cityInput,
        state: this.stateInput,
      };
      this.$emit("add-adress", payload);
      this.resetFields();
    },
  },
};
</script>
