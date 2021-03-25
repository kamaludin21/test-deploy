<template>
  <div
    :class="gender == 'female' ? 'bg-pink-200' : 'bg-blue-200'"
    class="flex flex-col w-full justify-center px-20 py-10 shadow-lg border mt-10"
  >
    <div class="flex w-full justify-center my-6">
      <img
        class="rounded-full border-2 border-white shadow-md h-32 w-32"
        :src="picture"
        alt=""
      />
    </div>
    <p class="text-2xl font-medium text-center w-full">
      {{ firstName }} {{ lastName }}
    </p>
    <p class="text-lg font-base text-center w-full">{{ email }}</p>
    <!-- Disable for a time after click -->
    <button
      id="myBtn"
      :class="isDisabled ? 'bg-gray-200' : 'bg-green-200'"
      class="border-2 shadow-lg py-2 px-4 bg-gray-300 my-2"
      v-on:click="getUsers()"
    >
      Get users, {{ isDisabled ? "wait" : "ready" }}
    </button>
  </div>
</template>


<script>
export default {
  name: "App",
  data() {
    return {
      isDisabled: false,
      clickCount: 0,
      firstName: "Jhon",
      lastName: "Doe",
      gender: "male",
      email: "jhon.doe@mail.com",
      picture: "https://randomuser.me/api/portraits/women/18.jpg",
    };
  },
  methods: {
    async getUsers() {
      if (this.isDisabled) return; // Button is disabled, halt block execution

      this.clickCount++;
      this.isDisabled = true;

      setTimeout(() => {
        this.isDisabled = false;
      }, 3000);

      const res = await fetch("https://randomuser.me/api");
      const { results } = await res.json();

      this.firstName = results[0].name.first;
      this.lastName = results[0].name.last;
      this.email = results[0].email;
      this.gender = results[0].gender;
      this.picture = results[0].picture.large;
    },
  },
};
</script>

