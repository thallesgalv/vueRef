<template>
  <div>
    <FormContainer @add-adress="handleAddAdress($event)" />
    <AdressContainer
      :list="orderedList"
      @delete-item="handleDeleteAdress($event)"
      @set-item-active="handleSetItemActive($event)"
    />
  </div>
</template>

<script>
import FormContainer from "../containers/FormContainer.vue";
import AdressContainer from "../containers/AdressContainer.vue";
import { v4 as uuid } from "uuid";

export default {
  name: "OptionsJsView",
  components: {
    FormContainer,
    AdressContainer,
  },
  data() {
    return {
      adressList: [],
    };
  },
  computed: {
    orderedList() {
      if (this.adressList?.length) {
        const ordered = [...this.adressList]
          .sort((a, b) => a.isActive - b.isActive)
          .reverse();
        return ordered;
      }
      return [];
    },
  },
  methods: {
    handleAddAdress(eventPayload) {
      if (eventPayload) {
        const newAdress = {
          id: uuid(),
          isActive: true,
          ...eventPayload,
        };

        this.adressListWithAnyActive();

        this.adressList.push(newAdress);
      }
    },
    handleDeleteAdress(id) {
      if (id) {
        this.adressList = this.adressList.filter((item) => item.id !== id);
      }
    },
    handleSetItemActive(id) {
      if (id) {
        this.adressListWithAnyActive();
        const finded = this.adressList.find((item) => item.id === id);

        if (finded) {
          this.handleDeleteAdress(finded.id);
          this.adressList = [...this.adressList, { ...finded, isActive: true }];
        }
      }
    },
    adressListWithAnyActive() {
      this.adressList = this.adressList.map((item) => {
        return { ...item, isActive: false };
      });
    },
  },
};
</script>
