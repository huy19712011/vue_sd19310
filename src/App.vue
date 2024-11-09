<script setup>
import { ref } from "vue";
const msg = ref("Hello from SD19310");
const newItem = ref("");
const newItemPriority = ref("low");

const iceCreamFlavors = ref(["vanilla"]);

const editing = ref(false);

const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value });

  newItem.value = "";
};

const items = ref([
  // { id: 1, label: "1 product A" },
  // { id: 2, label: "3 product B" },
  // { id: 3, label: "6 product C" },
]);

const doEdit = (e) => {
  editing.value = e;
  newItem.value = "";
};
</script>

<template>
  <div>
    <h1>{{ msg }}</h1>
    <br />
    <button
      v-if="editing"
      @click="doEdit(false)"
    >
      Cancel
    </button>
    <button
      v-else
      @click="doEdit(true)"
    >
      Add Item
    </button>
  </div>
  <br />

  <a v-bind:href="newItem">Dynamic Link</a>

  <form
    v-on:submit.prevent="saveItem"
    v-if="editing"
  >
    <input
      type="text"
      placeholder="Add an Item"
      v-model="newItem"
    />
    {{ newItem }} <br />

    Priority:
    <label>
      <input
        type="radio"
        value="low"
        v-model="newItemPriority"
      />
      Low
    </label>
    <label>
      <input
        type="radio"
        value="hight"
        v-model="newItemPriority"
      />
      Hight
    </label>
    <br />
    {{ newItemPriority }}

    <br />
    <label>
      <input
        type="checkbox"
        value="vanilla"
        v-model="iceCreamFlavors"
      />
      Vanilla
    </label>
    <label>
      <input
        type="checkbox"
        value="chocolate"
        v-model="iceCreamFlavors"
      />
      Chocolate
    </label>
    <label>
      <input
        type="checkbox"
        value="strawberry"
        v-model="iceCreamFlavors"
      />
      Strawberry
    </label>
    <br />
    {{ iceCreamFlavors }}
    <br />

    <button v-bind:disabled="newItem.length < 3">Save Item</button>
  </form>

  <ul>
    <li
      v-for="({ id, label }, index) in items"
      :key="id"
    >
      {{ index + 1 }} {{ label }} 😂
    </li>
  </ul>

  <p v-if="!items.length">Nothing to see here</p>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
