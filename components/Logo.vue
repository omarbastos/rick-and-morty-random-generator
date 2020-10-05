<template>
  <div class="container">
    <img
      class="logo"
      src="@/assets/Rick_and_Morty_logo.png"
      alt="Rick And Morty Logo"
    />
  </div>
</template>

<style>
.logo {
  animation: 1s appear;
  margin: auto;
  max-width: 100px;
}

@keyframes appear {
  0% {
    opacity: 0;
  }
}
</style>
