<template>
  <div class="card">
    <h2>{{ name }}</h2>
    <p>{{ description }}</p>
    <a :href="url" target="_blank">View Repository</a>
    <div v-if="topics.length">
      <h3>Topics:</h3>
      <ul>
        <li v-for="topic in topics" :key="topic">{{ topic }}</li>
      </ul>
    </div>
    <div v-if="license">
      <h3>License:</h3>
      <p>{{ license }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    description: String,
    url: String,
    topics: Array,
    license: String,
  },
};
</script>

<style>
.card {
  border: 1px solid #ccc;
  padding: 16px;
  margin: 16px 0;
  border-radius: 8px;
}
.card h2 {
  margin: 0 0 8px;
}
.card p {
  margin: 0 0 16px;
}
.card a {
  display: inline-block;
  margin-bottom: 16px;
  color: #007bff;
  text-decoration: none;
}
.card a:hover {
  text-decoration: underline;
}
.card ul {
  list-style-type: none;
  padding: 0;
}
.card li {
  background: #f1f1f1;
  display: inline-block;
  margin: 4px;
  padding: 4px 8px;
  border-radius: 4px;
}
</style>
