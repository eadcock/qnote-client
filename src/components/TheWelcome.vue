<script setup>

</script>

<template>
  <div class="wrapper">
    <h1>Welcome to qNote</h1>
    <RouterLink to="/login" class="link-button">Get Started</RouterLink>
  </div>
</template>

<style scoped>
  .link-button {
    display: inline-block;
    padding: 10px 20px;
    font-size: 16px;
    color: var(--color-text-dark);
    background-color: var(--color-blue);
    border: none;
    border-radius: 4px;
    text-align: center;
    text-decoration: none;
    cursor: pointer;
    transition: background-color 0.3s ease, color 0.3s ease;
  }

  h1 {
    color: var(--color-heading);
  }

  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }

  .link-button:hover {
    color: var(--color-text);
    background-color: var(--color-blue-dark);
  }
</style>
