<template>
  <section>
    <slot name="title">Users</slot>
    <slot
      name="userList"
      v-if="state === states.loaded"
      :list="data.results"
      :remove="remove"
      :count="data.results.length"
    >
      <ul class="userlist">
        <li v-for="user in data.results" :key="user.email">
          <slot name="listItem" :user="user">
            <div>
              <img
                width="48"
                height="48"
                :src="user.picture.large"
                :alt="user.name.first + ' ' + user.name.last"
              />
              <div>
                <div>{{ user.name.first }}</div>
                <!-- scoped slot -->
                <slot name="secondRow" :user="user" :remove="remove"></slot>
              </div>
            </div>
          </slot>
        </li>
      </ul>
    </slot>
    <slot name="idle" v-if="state === states.idle"> Idling... </slot>
    <slot name="loading" v-if="state === states.loading"> loading... </slot>
    <slot name="error" v-if="state === states.failed">
      Oops, something went wrong!
    </slot>
  </section>
</template>

<script>
const states = {
  idle: "idle",
  loading: "loading",
  loaded: "loaded",
  failed: "failed",
};
export default {
  props: { secondRow: { type: Function, default: () => {} } },
  data() {
    return {
      state: "idle",
      data: undefined,
      error: undefined,
      states,
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    async load() {
      this.state = "loading";
      this.error = undefined;
      this.data = undefined;
      try {
        const response = await fetch("https://randomuser.me/api/?results=5");
        const json = await response.json();
        this.state = states.loaded;
        this.data = json;
        return response;
      } catch (error) {
        this.state = states.failed;
        this.error = error;
        return error;
      }
    },
    remove(user) {
      this.data.results = this.data.results.filter(
        (entry) => entry.email !== user.email
      );
    },
  },
};
</script>

<style scoped>
.userlist {
  margin: 10px;
}
.userlist img {
  border-radius: 50%;
  margin-right: 1rem;
}
.userlist li + li {
  margin-top: 10px;
}
.userlist li > div {
  display: flex;
  align-items: center;
}
.userlist li div div {
  flex: 1;
}
</style>
