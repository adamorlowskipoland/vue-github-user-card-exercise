<template>
  <ul class="list-reset text-center">
    <li
      v-for="user in users"
      :key="user.id"
      class="my-3 p-3 shadow cursor-pointer border-l-4"
      :class="{'border-teal': isActive(user.slug)}"
      @click="chooseUser(user.slug)"
    >{{user.name}}</li>
  </ul>
</template>
<script>
export default {
  name: "UsersList",
  inject: ["user"],
  props: {
    users: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    isActive() {
      return slugText => slugText === this.user.nickname;
    }
  },
  methods: {
    chooseUser(slug) {
      this.user.nickname = slug;
    }
  }
};
</script>
