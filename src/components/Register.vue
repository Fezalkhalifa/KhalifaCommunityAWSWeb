<template>
    <div class="h-screen font-sans register bg-cover">
        <div class="container mx-auto h-full flex flex-1 justify-center items-center">
            <div class="w-full max-w-lg">
                <div class="leading-loose">
                    <form class="max-w-xl m-4 p-10 bg-white rounded shadow-xl">
                        <p class="text-gray-800 font-medium text-center box-content">Register</p>
                        <div class="">
                            <label class="block text-sm text-gray-00" for="cus_name">Name</label>
                            <input class="w-full px-5 py-1 text-gray-700 bg-gray-200 rounded" id="cus_name"
                                name="cus_name" type="text" v-model="Registration.Name" placeholder="Your Name"
                                aria-label="Name">
                        </div>
                        <div class="mt-2">
                            <label class="block text-sm text-gray-600" for="cus_email">Email</label>
                            <input class="w-full px-5  py-2 text-gray-700 bg-gray-200 rounded" id="cus_email"
                                name="cus_email" type="text" v-model="Registration.Email" placeholder="Your Email"
                                aria-label="Email">
                        </div>
                        <div class="mt-2">
                            <label class=" block text-sm text-gray-600" for="cus_address">Address</label>
                            <input class="w-full px-2 py-2 text-gray-700 bg-gray-200 rounded" id="cus_address"
                                name="cus_address" type="text" v-model="Registration.Address" placeholder="Street"
                                aria-label="Address">
                        </div>
                        <div class="mt-2">
                            <label class="text-sm block text-gray-600" for="cus_city">City</label>
                            <input class="w-full px-2 py-2 text-gray-700 bg-gray-200 rounded" id="cus_city"
                                name="cus_city" type="text" v-model="Registration.City" placeholder="City"
                                aria-label="City">
                        </div>
                        <div class="inline-block mt-2 w-1/2 pr-1">
                            <label class=" block text-sm text-gray-600" for="cus_country">Country</label>
                            <input class="w-full px-2 py-2 text-gray-700 bg-gray-200 rounded" id="cus_country"
                                name="cus_country" type="Country" v-model="Registration.Country" placeholder="Country"
                                aria-label="Country">
                        </div>
                        <div class="inline-block mt-2 -mx-1 pl-1 w-1/2">
                            <label class=" block text-sm text-gray-600" for="cus_zip">Zip</label>
                            <input class="w-full px-2 py-2 text-gray-700 bg-gray-200 rounded" id="cus_zip"
                                name="cus_zip" type="number" v-model="Registration.Zip" placeholder="Zip"
                                aria-label="Zip">
                        </div>
                        <div class="mt-2">
                            <label class=" block text-sm text-gray-600" for="cus_pw">Password</label>
                            <input class="w-full px-2 py-2 text-gray-700 bg-gray-200 rounded" id="cus_pw" name="cus_pw"
                                type="password" v-model="Registration.Users.Password" placeholder="Password"
                                aria-label="Password">
                        </div>
                        <div class="mt-2">
                            <label class=" block text-sm text-gray-600" for="cus_cpw">Confirm Password</label>
                            <input class="w-full px-2 py-2 text-gray-700 bg-gray-200 rounded" id="cus_cpw"
                                name="cus_cpw" type="password" v-model="Registration.Users.ConfirmPassword"
                                placeholder="Confirm Password" aria-label="Confirm Password">
                        </div>

                        <div class="mt-4">
                            <button v-on:click="SaveRegistration(Registration)"
                                class="px-4 py-1 text-white font-light tracking-wider text-center bg-gray-900 rounded"
                                type="button">Register</button>
                        </div>

                        <router-link
                            class="inline-block right-0 align-baseline font-bold text-sm text-500 hover:text-blue-800"
                            to="/login"> Already have an account ?
                        </router-link>
                    </form>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import router from "@/router";
export default {

    data: function () {
        return {
            Registration: {
                RegistrationId: 0,
                Name: '',
                Email: '',
                Address: '',
                City: '',
                Country: '',
                Zip: '',
                Users: {
                    UserId: 0,
                    RegistrationId: 0,
                    Password: '',
                    ConfirmPassword: '',
                },
            }
        }
    },
    methods: {
        SaveRegistration: function () {
            let uri ='http://khalifacommunitywebapilb-657308496.us-east-1.elb.amazonaws.com/Registration/CreateRegistration';
            //'https://localhost:44345/Registration/CreateRegistration'; //
            const Registration = {
                RegistrationId: this.Registration.RegistrationId,
                Name: this.Registration.Name,
                Email: this.Registration.Email,
                Address: this.Registration.Address,
                City: this.Registration.City,
                Country: this.Registration.Country,
                Zip: this.Registration.Zip,
                User: {
                    UserId: 0,
                    RegistrationId: 0,
                    Password: this.Registration.Users.Password,
                    ConfirmPassword: this.Registration.Users.Password,
                },
            }
            //this.axios.post(this.$options:{})
            this.axios.post(uri, Registration, {
   headers: {
    "Access-Control-Allow-Origin": "*"
        }
      }).then((response) => {
                if (response.data != null) {
                    var data = response.data;
                    if (data.messageType == 1) {
                        alert(data.message)
                        router.back();
                    }
                }
            }).catch((error) => {
                alert(error.message);
            });
        }

    },
    mounted() {
        console.log('Register mounted')
    }
};
</script>