<template>
  <div id="nav" class="nav">
    <router-link v-bind:to="{ name: 'home' }">
      <img src="https://i.imgur.com/rBJDZci.png" class="image" />
    </router-link>

    <div id="dark-nav">
      <router-link
        v-bind:to="{ name: 'updatepets' }"
        v-if="$store.state.token != ''"
        class="dark-item"
      >
        Update Pets
      </router-link>
      <router-link
        v-bind:to="{ name: 'applicants' }"
        class="dark-item"
        v-if="toggleAdmin"
      >
        Applicants
      </router-link>
    </div>

    <div class="nav-items">
      <router-link v-bind:to="{ name: 'adopt' }" class="nav-item">
        Adopt
      </router-link>

      <div>
        <router-link
          v-bind:to="{ name: 'logout' }"
          v-if="$store.state.token != ''"
          class="nav-item"
        >
          Logout
        </router-link>

        <router-link
          v-bind:to="{ name: 'logout' }"
          v-if="$store.state.token === ''"
          class="nav-item"
        >
          Login
        </router-link>
      </div>

      <button class="volunteerList">
        <router-link
          v-bind:to="{ name: 'volunteer' }"
          v-if="$store.state.token === ''"
          class="nav-item"
        >
          Volunteer
        </router-link>

        <router-link
          v-bind:to="{ name: 'directory' }"
          v-if="$store.state.token != ''"
          class="nav-item"
        >
          Directory
        </router-link>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "nav-bar",
  data() {
    return {};
  },

  computed: {
    toggleAdmin() {
      const isAdmin =
        this.$store.state.token !== "" &&
        this.$store.state.user.authorities[0].name === "ROLE_ADMIN"
          ? true
          : false;
      return isAdmin;
    },
  },
};
</script>

<style scoped>
.nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100px;
  padding-left: 20px;
}

.image {
  max-height: 70px;
}

#dark-nav {
  display: flex;
  width: 45%;
  flex-direction: row-reverse;
  font-size: 25px;
  height: 100%;
  align-items: center;
}

.nav-items {
  display: flex;
  width: 35%;
  justify-content: space-between;
  align-items: center;
  font-size: 25px;
  margin-right: 50px;
  height: 100%;
}

.nav-item {
  text-transform: uppercase;
  font-weight: 700;
  color: #f2ebe6;
  text-decoration: none;
}

.dark-item {
  font-size: 25px;
  text-transform: uppercase;
  font-weight: 800;
  text-decoration: none;
  color: #335137;
  margin-left: 50px;
}

.volunteerList {
  color: white;
  font-weight: bold;
}

button {
  border-radius: 50px;
  border: none;
  padding: 10px 30px;
  background-color: #de854e;
  font-size: 25px;
  padding: 10px 30px;
  text-transform: uppercase;
  text-decoration: none;
}
</style>
