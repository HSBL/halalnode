<template>
  <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
    <a class="navbar-brand" href="#">Halal Node Front End Challenge</a>
    <form class="form-inline">
      <button class="btn btn-outline-success" type="button" v-on:click="signin">Sign in</button>
      <button class="btn btn-outline-danger" type="button" v-if="output" v-on:click="logout">Log out</button>
    </form>
  </nav>
</template>
<script>
export default {
  props: {
    output: {
      type: Object
    }
  },
  data() {
    return {
      //   info: null
      result: null
    };
  },
  methods: {
    signin: function() {
      this.$emit("emitSignin");
    },
    logout: function() {
      let currentObj = this;
      this.$http
        .delete("https://api.halalnode.com:8250/v1/accounts/logout", {
          headers: {
            Authorization: "Bearer " + this.output.data.accessToken
          }
        })
        .then(function(response) {
          currentObj.result = response.data;
          alert(currentObj.result.message);
        })
        .catch(function(error) {
          currentObj.result = error;
        });
    }
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
