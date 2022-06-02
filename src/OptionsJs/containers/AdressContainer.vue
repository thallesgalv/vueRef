<template>
  <section>
    <div v-if="list.length">
      <ul>
        <li v-for="item in list" :key="item.id">
          <AdressItem
            :info="item"
            @delete="handleDelete($event)"
            @set-active="handleSetActive($event)"
          />
        </li>
      </ul>
    </div>
    <div v-else>
      <p>Não há nenhum endereço cadastrado.</p>
    </div>
  </section>
</template>

<script>
import AdressItem from "../components/AdressItem.vue";
export default {
  name: "AdressContainer",
  components: {
    AdressItem,
  },
  props: {
    list: {
      type: Array,
      required: true,
    },
  },
  methods: {
    handleDelete(evt) {
      this.$emit("delete-item", evt);
    },

    handleSetActive(evt) {
      this.$emit("set-item-active", evt);
    },
  },
};
</script>
