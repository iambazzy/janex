<template>
  <v-row no-gutters>
    <v-col v-if="$vuetify.breakpoint.mdAndUp" cols="7" class="bg">
      <div class="overlay pa-10 d-flex flex-column justify-space-between">
        <logo />

        <p class="white--text description">
          A platform which allows users <br />
          to quickly and securely bridge <br />
          assets from any blockchain.
        </p>
      </div>
    </v-col>

    <v-col
      cols="12"
      md="5"
      class="pa-3 pa-md-16 form d-flex justify-center align-center"
      v-if="showThanks"
    >
      <h2 class="pt-6 white--text">Thanks for signing up!</h2>
    </v-col>

    <v-col v-else cols="12" md="5" class="pa-3 pa-md-16 form">
      <logo v-if="$vuetify.breakpoint.smAndDown" />

      <div class="greetings pt-8 pt-md-14">
        <h1 class="white--text">Create an account.</h1>
        <small class="sub-heading">
          Please fill in the details below to create an account
        </small>
      </div>

      <register-form class="pt-6" @submitted="showSubmitted" />
    </v-col>
  </v-row>
</template>

<script>
import RegisterForm from '@/components/RegisterForm.vue'
import Logo from '@/components/Logo.vue'

export default {
  name: 'Home',

  components: {
    RegisterForm,
    Logo
  },

  data() {
    return {
      showThanks: false
    }
  },
  
  methods: {
    showSubmitted() {
      this.showThanks = true;
    }
  }
}
</script>

<style scoped lang="scss">
.bg {
  background: url("../assets/image2.webp");
  background-repeat: no-repeat;
  background-size: cover;
  .overlay {
    background: rgba(4, 2, 31, 0.6);
    height: 100%;
  }
  .description {
    width: 491px;
    font-size: 24px;
    font-weight: 600;
  }
}

.form {
  background-color: #04021f;

  .greetings {
    line-height: 25px;

    .sub-heading {
      padding-left: 2px;
      color: #969696;
    }
  }
}
</style>
