<template>
  <div class="not-found">
    <h1>404 - Page Not Found</h1>
    <p>Sorry, the page you are looking for does not exist.</p>
    <router-link to="/">Go back to Home</router-link>
  </div>
</template>

<script setup lang="ts"></script>
<style>
.not-found {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  background-color: #f8d7da;
  color: #721c24;
}

.not-found h1 {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.not-found p {
  font-size: 1.25rem;
  margin-bottom: 2rem;
}

.not-found a {
  padding: 0.5rem 1rem;
  background-color: #cce5ff;
  color: #004085;
  text-decoration: none;
  border-radius: 5px;
}

.not-found a:hover {
  background-color: #b8daff;
}

@media (min-width: 1024px) {
  .not-found {
    min-height: 100vh;
  }
}
</style>
