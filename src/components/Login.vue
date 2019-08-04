<template>
  <div>
    <form class="form-signin">
      <h3>Sign in</h3>

      <div class="form-label-group">
        <input
          ref="user"
          type="text"
          id="inputEmail"
          class="form-control"
          placeholder="Username"
          required
          autofocus
        />
        <label for="inputEmail">Username</label>
      </div>

      <div class="form-label-group">
        <input
          ref="password"
          type="password"
          id="inputPassword"
          class="form-control"
          placeholder="Password"
          required
        />
        <label for="inputPassword">Password</label>
      </div>
      <button
        class="btn btn-lg btn-primary btn-block"
        v-on:click.prevent="submitSignin"
        type="submit"
      >Sign in</button>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      output: "",
    };
  },
  methods: {
    submitSignin: function() {
      let currentObj = this;
      this.$http
        .post("https://api.halalnode.com:8250/v1/accounts/login", {
          identity: this.$refs.user.value,
          password: this.$refs.password.value,
          registrationToken: "",
          admin: false,
          staySignedIn: false
        })
        .then(function(response) {
          currentObj.output = response.data;
          currentObj.successSignin();
        })
        .catch(function(error) {
          currentObj.output = error;
        });
    },
    successSignin: function() {
      this.$emit("emitSignedin", this.output);
    }
  },
  mounted() {
    // this.$http
    //   .get("https://api.coindesk.com/v1/bpi/currentprice.json")
    //   .then(response => (this.info = response));
  }
};
</script>

<style lang="scss" scoped>
.form-signin {
  width: 100%;
  max-width: 420px;
  padding: 15px;
  margin: auto;
}

.form-label-group {
  position: relative;
  margin-bottom: 1rem;
}

.form-label-group > input,
.form-label-group > label {
  height: 3.125rem;
  padding: 0.75rem;
}

.form-label-group > label {
  position: absolute;
  top: 0;
  left: 0;
  display: block;
  width: 100%;
  margin-bottom: 0; /* Override default `<label>` margin */
  line-height: 1.5;
  color: #495057;
  pointer-events: none;
  cursor: text; /* Match the input under the label */
  border: 1px solid transparent;
  border-radius: 0.25rem;
  transition: all 0.1s ease-in-out;
}

.form-label-group input::-webkit-input-placeholder {
  color: transparent;
}

.form-label-group input:-ms-input-placeholder {
  color: transparent;
}

.form-label-group input::-ms-input-placeholder {
  color: transparent;
}

.form-label-group input::-moz-placeholder {
  color: transparent;
}

.form-label-group input::placeholder {
  color: transparent;
}

.form-label-group input:not(:placeholder-shown) {
  padding-top: 1.25rem;
  padding-bottom: 0.25rem;
}

.form-label-group input:not(:placeholder-shown) ~ label {
  padding-top: 0.25rem;
  padding-bottom: 0.25rem;
  font-size: 12px;
  color: #777;
}
</style>

