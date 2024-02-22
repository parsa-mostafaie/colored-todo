<template>
  <div>
    <slot></slot>
  </div>
</template>

<style scoped>
div {
  width: 45%;
  margin: 0 auto;
}

@media only screen and (max-width: 840px) {
  div {
    width: 70%;
  }
}

@media only screen and (max-width: 576px) {
  div {
    width: 100%;
  }
}
</style>
