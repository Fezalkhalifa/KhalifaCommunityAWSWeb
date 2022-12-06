<template>
  <div class="h-max mt-0 font-sans login bg-cover">
    <div class="container mx-auto h-full flex flex-1 justify-center items-center">
      <div class="w-full max-w-lg">
        <div class="leading-loose">
          <form class="max-w-xl m-4 p-10 bg-white rounded shadow-xl">
            <p class="text-gray-800 text-center text-lg font-bold">Login</p>
            <div class="">
              <label class="block text-sm text-gray-00" for="username">Username</label>
              <input class="w-full px-5 py-1 text-gray-700 bg-gray-200 rounded" id="email" name="email" type="text"
                v-model="email" placeholder="email" aria-label="email" />
            </div>
            <div class="mt-2">
              <label class="block text-sm text-gray-600" for="password">Password</label>
              <input class="w-full px-5 py-1 text-gray-700 bg-gray-200 rounded" id="password" name="password"
                type="password" placeholder="*******" v-model="Password" aria-label="password" />
            </div>
            <div class="mt-4 items-center justify-between">
              <button class="
                  px-4
                  py-1
                  text-white
                  font-light
                  tracking-wider
                  bg-gray-900
                  rounded
                " type="button" v-on:click="Submit($event)">
                Login
              </button>
            </div>
            <router-link class="
                inline-block
                right-0
                align-baseline
                font-bold
                text-sm text-500
                hover:text-blue-800
              " to="/register">
              Not registered ?
            </router-link>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import router from '../router';
                
export default {
  data: function () {
    return {
      email: ''
    }
  },
  mounted() {
    console.log("Login mounted");
  },
  methods: {
    Submit: async function (e) {
      e.preventDefault()
      let uri = 'http://khalifacommunitywebapilb-657308496.us-east-1.elb.amazonaws.com/Registration/Login?email=' + this.email;
      var response = await this.axios.post(uri).then((response) => {
        if (response.data != null) {
          var data = response.data;
          return data;
        }
      }).catch((error) => {
        alert(error.message);
      });

      if (response != null) {
        if (response.messageType == 1) {
          alert(response.message);
          router.push('/')
        }else{
          alert(response.message);
        }
      }
    }
  }
};
</script>