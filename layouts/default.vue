<template>
    <div class="layout">
      <AppHeader />
      <slot />
      <AppFooter />
    </div>
</template>
<style scoped>
.layout {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
