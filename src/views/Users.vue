<template>
  <div class="page">
    <select v-model="selected">
      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
      >
        {{ option.label }}
      </option>
    </select>
    <app-user-list>
      <template #loading>
        <app-spinner />
      </template>
      <template #userList="{ remove, list }">
        <user-cards-list :list="list">
          <template #[selected]="{ text }">
            <h4>{{ text }}</h4>
          </template>
          <template #secondRow="{ user }">
            <app-button @click="remove(user)">Remove</app-button>
          </template>
        </user-cards-list>
      </template>
    </app-user-list>
  </div>
</template>

<script>
// @ is an alias to /src
import AppUserList from "@/components/AppUserList.vue";
import AppSpinner from "@/components/AppSpinner.vue";
import UserCardsList from "@/components/AppUserCardsList.vue";
import AppButton from "@/components/AppButton.vue";

export default {
  name: "Home",
  components: {
    AppUserList,
    AppSpinner,
    // eslint-disable-next-line vue/no-unused-components
    UserCardsList,
    AppButton,
  },
  data() {
    return {
      selected: "first",
      options: [
        { value: "first", label: "first name" },
        { value: "last", label: "last name" },
        { value: "full", label: "full name" },
        { value: "fullWithTitle", label: "full name with title" },
      ],
    };
  },
};
</script>

<style scoped>
.page {
  padding: 2rem;
}
.page > * + * {
  margin-top: 2rem;
}
</style>
