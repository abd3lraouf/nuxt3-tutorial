<template>
  <a :href="url" target="_blank" class="card">
    <div class="card-content">
      <h2 class="card-title">{{ name }}</h2>
      <p class="card-description">{{ description }}</p>
      <div v-if="topics.length" class="card-topics">
        <h3>Topics:</h3>
        <ul>
          <li v-for="topic in topics" :key="topic">
            <UBadge color="gray" variant="solid">{{ topic }}</UBadge>
          </li>
        </ul>
      </div>
      <div v-if="license" class="card-license">
        <h3>License</h3>
        <p>{{ license }}</p>
      </div>
    </div>
  </a>
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
  @apply font-mono;
  display: block;
  text-decoration: none;
  color: inherit;
  margin: 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 16px;
  transition: box-shadow 0.3s ease;
  word-wrap: break-word; /* Ensure long words are wrapped */
  overflow-wrap: break-word; /* Ensure long words are wrapped */
}

.card:hover {
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.card-content {
  display: flex;
  flex-direction: column;
}

.card-title {
  font-size: 1.5em;
  margin-bottom: 8px;
  word-wrap: break-word; /* Ensure long words are wrapped */
  overflow-wrap: break-word; /* Ensure long words are wrapped */
}

.card-description {
  font-size: 1em;
  margin-bottom: 16px;
  word-wrap: break-word; /* Ensure long words are wrapped */
  overflow-wrap: break-word; /* Ensure long words are wrapped */
}

.card-topics {
  margin-bottom: 16px;
}

.card-topics h3 {
  font-size: 1.2em;
  margin-bottom: 8px;
}

.card-topics ul {
  @apply flex flex-row flex-wrap gap-x-4;
  list-style-type: none;
}

.card-topics li {
  @apply mb-2 inline-block;
  font-size: 1em;
}

.card-license h3 {
  font-size: 1.2em;
  margin-bottom: 8px;
  word-wrap: break-word; /* Ensure long words are wrapped */
  overflow-wrap: break-word; /* Ensure long words are wrapped */
}

.card-license p {
  font-size: 1em;
  word-wrap: break-word; /* Ensure long words are wrapped */
  overflow-wrap: break-word; /* Ensure long words are wrapped */
}
</style>
