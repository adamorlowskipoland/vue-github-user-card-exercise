<template>
  <div id="app">
    <div class="container mx-auto pt-8">
      <div class="flex mb-4 -mx-2">
        <div class="w-1/2 h-12 p-2 text-center">
          <h3 class="text-2xl mb-5 uppercase">Choose a github User</h3>
          <UsersList :users="users"/>

          <div class="mt-5">
            <button
              class="bg-transparent hover:bg-pink text-pink-dark font-semibold hover:text-white py-2 px-4 border border-pink hover:border-transparent rounded"
              @click="user.nickname = null"
            >Reset</button>
          </div>
        </div>
        <div class="w-1/2 p-2 text-center">
          <h3 v-if="!user.nickname" class="text-2xl mb-5 uppercase">You will see his card here</h3>
          <FetchData v-else :endpoint="userEndpoint">
            <div slot-scope="{data: user, error, pending}">
              <div>
                <UserCard
                  v-if="user"
                  :imgUrl="user.avatar_url"
                  :imgAlt="`${user.name} avatar`"
                  :name="user.name"
                  :description="user.bio"
                  :location="user.location"
                  :created="user.created_at"
                  :followers="user.followers"
                />
              </div>
              <div v-if="pending">
                <img
                  src="http://www.sageflyfish.com/resources/admin/widgets/loading.gif"
                  alt="loading"
                  class="loader"
                >
                <p>Loading...</p>
              </div>
              <h3 v-if="error" style="color: red;">{{error}}</h3>
            </div>
          </FetchData>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import FetchData from "./components/FetchData";
import UserCard from "./components/UserCard";
import UsersList from "./components/UsersList";

export default {
  name: "App",
  provide() {
    return {
      user: this.user
    };
  },
  components: {
    UserCard,
    FetchData,
    UsersList
  },
  data() {
    return {
      baseEndpoint: "https://api.github.com",
      baseEndpointUsers: "https://api.github.com/users",
      user: {
        nickname: null
      },
      users: [
        {
          id: 2,
          name: "Adam (me :-D )",
          slug: "adamorlowskipoland"
        },
        {
          id: 1,
          name: "Hootlex (guy from vue-school)",
          slug: "hootlex"
        },
      ]
    };
  },
  computed: {
    userEndpoint() {
      return this.user.nickname
        ? `${this.baseEndpointUsers}/${this.user.nickname}`
        : "";
    }
  }
};
</script>
