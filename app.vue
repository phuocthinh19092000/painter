<template>
  <div>
    <n-config-provider :theme-overrides="themeOverrides">
      <NuxtLayout>
        <NuxtPage />
      </NuxtLayout>
    </n-config-provider>
  </div>
</template>
<script>
import { NConfigProvider } from 'naive-ui'
export default {
  name: "App",
  components: {
    NConfigProvider
  },
  // data() {
  //   return {
  //     themeOverrides: {
  //       common: {
  //         primaryColor: '#FF0000'
  //       },
  //       Button: {
  //         textColor: '#000000'
  //       },
  //     }
  //   }
  // }
}
</script>

