<template>
  <div>
    <h1>Projects</h1>
    <UButton color="green" @click="switchToSuccess()">Load success</UButton>
    <UButton color="red" @click="switchToError()">Load error</UButton>

    <div v-if="loading" class="loading-container">
      <div class="loading-card">
        <div class="spinner"></div>
        <p class="loading-text">Loading <span class="dots"></span></p>
      </div>
    </div>
    <div v-else-if="error || !success" class="error-container">
      <UAlert
        icon="i-material-symbols-warning"
        color="red"
        variant="subtle"
        title="Error loading data!"
        description="An error occurred while loading the data. Please try again later."
      />
    </div>
    <div v-else>
      <ul class="grid grid-cols-2 gap-4">
        <li v-for="project in projects">
          <Project
            :key="project.id"
            :name="project.name"
            :description="project.description"
            :url="project.html_url"
            :topics="project.topics"
            :license="project.license?.name"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, watchEffect } from "vue";
import Project from "./project.vue";

// Define the type for a project
interface ProjectType {
  id: number;
  name: string;
  description: string;
  html_url: string;
  topics: string[];
  license: { name: string } | null;
}

const projects = ref<ProjectType[]>([]);
const loading = ref(true);
const success = ref(false);
const error = ref(false);
const delay = (ms: number) => new Promise((resolve) => setTimeout(resolve, ms));

const fetchData = async (url: string) => {
  loading.value = true;
  success.value = false;
  error.value = false;
  await delay(2000);
  const { status, data } = useFetch<ProjectType[]>(url, {
    onResponse: (ctx) => {
      if (ctx.response.status === 200) {
        projects.value = ctx.response._data ?? [];
        success.value = true;
      } else {
        success.value = false;
      }
      loading.value = false;
    },
  });
  watchEffect(() => {
    if (status.value === "pending") {
      loading.value = true;
    } else if (status.value === "success") {
      if (data.value) {
        projects.value = data.value;
        success.value = true;
      } else {
        error.value = true;
      }
      loading.value = false;
    } else {
      error.value = true;
      loading.value = false;
    }
  });
};

const switchToSuccess = () => {
  fetchData("https://api.github.com/users/abd3lraouf/repos");
};

const switchToError = () => {
  fetchData("https://api.github.com/users/abd3lraouf/invalid-path");
};
</script>

<style>
.loading-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.loading-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  background-color: #fff;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid transparent;
  border-top: 4px solid #3498db;
  border-radius: 50%;
  animation:
    spin 1s linear infinite,
    color-change 4s linear infinite;
  margin-bottom: 10px;
}

.loading-text {
  font-size: 1.2em;
  margin-top: 10px;
}

.dots::after {
  content: "";
  display: inline-block;
  width: 1em;
  text-align: left;
  animation: dots 2s steps(4, end) infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes color-change {
  0% {
    border-top-color: #3498db;
  }
  25% {
    border-top-color: #e74c3c;
  }
  50% {
    border-top-color: #f1c40f;
  }
  75% {
    border-top-color: #2ecc71;
  }
  100% {
    border-top-color: #3498db;
  }
}

@keyframes dots {
  0%,
  20% {
    content: ".";
  }
  40% {
    content: "..";
  }
  60% {
    content: "...";
  }
  80%,
  100% {
    content: "....";
  }
}

.error-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
