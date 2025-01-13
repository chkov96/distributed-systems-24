<template>
  <div class="container">
    <h1>Shopping List Manager</h1>

    <!-- Success and error messages -->
    <div v-if="messages.length">
      <div v-for="(msg, index) in messages" :key="index" :class="`alert ${msg.type}`">
        {{ msg.text }}
      </div>
    </div>

    <!-- Shopping list table -->
    <h2>All Shopping Items</h2>
    <table>
      <thead>
        <tr>
          <th>Item Name</th>
          <th>Quantity</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.id">
          <td>{{ item.name }}</td>
          <td>{{ item.amount }}</td>
        </tr>
      </tbody>
    </table>

    <!-- Add a new item -->
    <h2>Add a New Item</h2>
    <form @submit.prevent="addItem">
      <input type="text" v-model="newItem.name" placeholder="Enter item name" required />
      <input type="number" v-model="newItem.amount" placeholder="Enter quantity" required />
      <button type="submit">Add Item</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [], // Shopping list item
      messages: [], // Success/error messages
      newItem: { name: "", amount: 0 }, // New item
    };
  },
  async fetch() {
    // Fetch items from the API
    try {
      const response = await this.$axios.$get('/items');
      this.items = response;
    } catch (error) {
      this.messages.push({ type: 'error', text: 'Error fetching items.' });
    }
  },
  methods: {
    async addItem() {
      // Send new item to the API
      try {
        await this.$axios.$post('/items', this.newItem);
        this.messages.push({ type: 'success', text: 'Item added successfully!' });
        this.newItem = { name: "", amount: 0 }; // Reset the form
        await this.fetch(); // Refresh the list
      } catch (error) {
        this.messages.push({ type: 'error', text: 'Error adding item.' });
      }
    },
  },
};
</script>

<template>
  <div class="container">
    <h1>Shopping List Manager</h1>

    <!-- Success and error messages -->
    <div v-if="messages.length">
      <div v-for="(msg, index) in messages" :key="index" :class="`alert ${msg.type}`">
        {{ msg.text }}
      </div>
    </div>

    <!-- Shopping list table -->
    <h2>All Shopping Items</h2>
    <table>
      <thead>
        <tr>
          <th>Item Name</th>
          <th>Quantity</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in items" :key="item.id">
          <td>{{ item.name }}</td>
          <td>{{ item.amount }}</td>
        </tr>
      </tbody>
    </table>

    <!-- Add a new item -->
    <h2>Add a New Item</h2>
    <form @submit.prevent="addItem">
      <input type="text" v-model="newItem.name" placeholder="Enter item name" required />
      <input type="number" v-model="newItem.amount" placeholder="Enter quantity" required />
      <button type="submit">Add Item</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [], // Shopping list items
      messages: [], // Success/error messages
      newItem: { name: "", amount: 0 }, // New item
    };
  },
  async fetch() {
    // Fetch items from the API
    try {
      const response = await this.$axios.$get('/items');
      this.items = response;
    } catch (error) {
      this.messages.push({ type: 'error', text: 'Error fetching items.' });
    }
  },
  methods: {
    async addItem() {
      // Send new item to the API
      try {
        await this.$axios.$post('/items', this.newItem);
        this.messages.push({ type: 'success', text: 'Item added successfully!' });
        this.newItem = { name: "", amount: 0 }; // Reset the form
        await this.fetch(); // Refresh the list
      } catch (error) {
        this.messages.push({ type: 'error', text: 'Error adding item.' });
      }
    },
  },
};
</script>

<style src="./styles.css"></style>

</style>
