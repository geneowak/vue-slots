<template>
  <app-layout>
    <template v-slot:header>some header</template>
    <app-button>
      body there
      <AppIcon />
    </app-button>
    <template #footer>This is a footer</template>
  </app-layout>
</template>

<script>
// @ is an alias to /src
import AppLayout from "@/components/AppLayout.vue";
import AppButton from "@/components/AppButton.vue";
import AppIcon from "@/components/AppIcon";

export default {
  name: "Home",
  components: {
    AppLayout,
    AppButton,
    AppIcon,
  },
};
</script>
