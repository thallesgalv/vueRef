<template>
  <div>
    <p>{{ info.isActive }}</p>
    <p v-if="info.street">{{ info.street }}</p>
    <p v-if="info.zipCode">{{ info.zipCode }}</p>
    <p v-if="info.neighborhood">{{ info.neighborhood }}</p>
    <p v-if="info.city">{{ info.city }}</p>
    <p v-if="info.state">{{ info.state }}</p>
    <button @click="emitSetActive(info.id)">Set ative</button>
    <button @click="emitDelete(info.id)">Delete</button>
  </div>
</template>

<script>
export default {
  name: "AdressItem",
  props: {
    info: {
      type: Object,
      required: true,
    },
  },
  methods: {
    emitDelete(id) {
      this.$emit("delete", id);
    },
    emitSetActive(id) {
      this.$emit("set-active", id);
    },
  },
};
</script>
