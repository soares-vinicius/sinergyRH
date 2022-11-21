<template>
  <div class="container">
    <div class="item">
      <h2>
        <slot name="heading"></slot>
      </h2>
      <div class="details">
        <slot></slot>
      </div>
      <i>
        <slot name="icon"></slot>
      </i>
    </div>
  </div>
</template>

<style scoped>
.item {
  position: relative;
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 25px;
  display: flex;
  flex-direction: column;
  box-shadow: 0 0 15px 0px rgba(0, 0, 0, 0.25);
  clip-path: inset(0px -15px 0px -15px);
  position: relative;
}

.details {
  color: var(--white);
  font-size: 1.563rem;
  line-height: 2.375rem;
  margin-top: 30px;
}

h2 {
  font-size: 1.875rem;
  line-height: 2.813rem;
  font-weight: 800;
  color: var(--white);
}

i {
  max-width: 600px;
  width: 100%;
  max-height: 600px;
  height: 100%;
  margin: 30px auto;
}
</style>
