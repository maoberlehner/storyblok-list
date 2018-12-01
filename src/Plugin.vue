<template>
  <div class="List">
    <ol class="List__list uk-margin-bottom-remove">
      <li
        v-for="(item, index) in model.items"
        :key="index"
        class="List__list-item"
      >
        <input
          v-model="model.items[index]"
          :aria-label="`List item ${index}`"
          class="uk-form-small uk-width-1-1"
        >
      </li>
    </ol>
    <a
      class="blok__full-btn uk-margin-small-top"
      @click="addItem"
    >
      <i class="uk-icon-plus-circle uk-margin-small-right"/>
      Add item
    </a>
  </div>
</template>

<script>
export default {
  mixins: [window.Storyblok.plugin],
  watch: {
    model: {
      deep: true,
      handler(value) {
        this.$emit(`changed-model`, value);
      },
    },
  },
  methods: {
    addItem() {
      this.model.items.push(``);
    },
    initWith() {
      return {
        items: [``],
        plugin: `list`,
      };
    },
  },
};
</script>

<style>
.List__list {
  padding-left: 0;
}

.List__list-item + .List__list-item {
  margin-top: 5px;
}
</style>
