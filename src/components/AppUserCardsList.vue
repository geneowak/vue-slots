<template>
  <ul class="userlist">
    <li v-for="user in list" :key="user.email">
      <slot name="listItem" :user="user">
        <div class="card">
          <img
            class="resposive"
            :src="user.picture.large"
            :alt="user.name.first + ' ' + user.name.last"
          />
          <div class="card-body">
            <slot name="first" :text="user.name.first"></slot>
            <slot name="last" :text="user.name.last"></slot>
            <slot
              name="full"
              :text="`${user.name.first} ${user.name.last}`"
            ></slot>
            <slot
              name="fullWithTitle"
              :text="`${user.name.title} ${user.name.first} ${user.name.last}`"
            ></slot>
            <slot name="secondRow" :user="user"></slot>
          </div>
        </div>
      </slot>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    list: Array,
    default: () => {},
  },
};
</script>

<style scoped>
.userlist {
  display: grid;
  gap: 1rem;
  grid-template-columns: 1fr 1fr 1fr;
}
.resposive {
  width: 100%;
}
.card {
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.25);
  border-radius: 4px;
  overflow: hidden;
}
.card-body {
  padding: 1rem;
}
</style>
