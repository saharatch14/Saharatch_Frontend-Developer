<template>
  <div class="user-list-container">
    <button @click="toggleSort" class="sort-btn">
      Sort by Age: {{ isDescending ? 'Descending' : 'Ascending' }}
    </button>

    <table border="1" class="user-table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Email</th>
          <th>Age</th>
          <th>Role</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in sortedUsers" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.age }}</td>
          <td>{{ user.role }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    users: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      // Default state is false (Ascending)
      isDescending: false
    };
  },
  computed: {
    // Computed property to handle logic reactively
    sortedUsers() {
      // Create a copy of the prop to avoid direct mutation
      const usersCopy = [...this.users];
      
      return usersCopy.sort((a, b) => {
        if (this.isDescending) {
          return b.age - a.age; // Descending
        }
        return a.age - b.age; // Ascending
      });
    }
  },
  methods: {
    toggleSort() {
      this.isDescending = !this.isDescending;
    }
  }
};
</script>

<style scoped>
.user-list-container {
  padding: 20px;
}
.sort-btn {
  margin-bottom: 15px;
  padding: 8px 16px;
  cursor: pointer;
}
.user-table {
  width: 100%;
  border-collapse: collapse;
}
.user-table th, .user-table td {
  padding: 10px;
  text-align: left;
}
</style>