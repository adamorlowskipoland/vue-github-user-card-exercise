<template functional>
  <div
    class="user-card mx-auto max-w-xs p-2 bg-grey-lighter max-w-xs rounded overflow-hidden shadow-lg text-center"
  >
    <img :src="props.imgUrl" :alt="props.imgAlt" class="w-full">
    <div class="px-6 py-4">
      <div class="font-bold text-xl mt-2">{{props.name}}</div>
      <p class="text-grey-darker text-xs mt-2">Joined in {{props.created}}</p>
      <p class="text-grey-darker text-xs mt-2">{{props.description}}</p>
      <p class="text-grey-darker text-xs mt-2">Location: {{props.location}}</p>
    </div>
    <span
      class="inline-block bg-teal-lighter rounded-full px-3 py-1 text-sm font-semibold text-grey-darker"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
        fill="currentColor"
        class="w-3 h-3"
      >
        <path
          d="M5 5a5 5 0 0 1 10 0v2A5 5 0 0 1 5 7V5zM0 16.68A19.9 19.9 0 0 1 10 14c3.64 0 7.06.97 10 2.68V20H0v-3.32z"
        ></path>
      </svg>
      {{followers}} {{props.followers.length > 1 ? 'follower' : 'followers'}}
    </span>
  </div>
</template>

<script>
export default {
  name: "UserCard",
  props: {
    imgUrl: {
      type: String,
      default: ""
    },
    imgAlt: {
      type: String,
      default: "Image avatar"
    },
    name: {
      type: String,
      default: ""
    },
    description: {
      type: String,
      default: ""
    },
    location: {
      type: String,
      default: ""
    },
    created: {
      type: String,
      default: ""
    },
    followers: {
      type: Number,
      default: 0
    }
  }
};
</script>
