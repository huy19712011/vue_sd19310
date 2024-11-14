<script setup>
import { ref, computed } from "vue";
const msg = ref("Hello from SD19310");
const characterCount = computed(() => {
  return newItem.value.length;
});
const newItem = ref("");
const newItemPriority = ref("low");

const iceCreamFlavors = ref(["vanilla"]);

const editing = ref(false);

const saveItem = () => {
  items.value.push({ id: items.value.length + 1, label: newItem.value });

  newItem.value = "";
};

const items = ref([
  { id: 1, label: "1 product A", purchased: false, highPriority: false },
  { id: 2, label: "3 product B", purchased: false, highPriority: false },
  { id: 3, label: "6 product C", purchased: true, highPriority: true },
]);

const reverseItems = computed(() => {
  return [...items.value].reverse();
});

const doEdit = () => {
  editing.value = !editing.value;
  newItem.value = "";
};

const togglePurchased = (item) => {
  item.purchased = !item.purchased;
};
</script>

<template>
  <div>
    <h1>{{ msg }}</h1>
    <br />
    <button
      v-if="editing"
      @click="doEdit()"
    >
      Cancel
    </button>
    <button
      class="btn btn-primary"
      v-else
      @click="doEdit()"
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
  <br />
  {{ characterCount }}
  <br />

  <ul>
    <li
      v-for="({ id, label, purchased, highPriority }, index) in reverseItems"
      @click="togglePurchased(items[index])"
      :key="id"
      :class="{ strikeout: purchased, priority: highPriority }"
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
