<template>
  <section class="resume-section p-3 p-lg-5 d-flex flex-column" id="contact">
    <div>
      <form class="vue-form" @submit.prevent="submit">
        <div class="error-message">
          <p v-show="!email.valid">Oh, please enter a valid email address.</p>
        </div>
        <fieldset>
          <h2 class="mb-5">Contact Me</h2>
          <div>
            <label class="label" for="name">Name</label>
            <input type="text" name="name" id="name" required="" v-model="name">
          </div>
          <div>
            <label class="label" for="email">Email</label>
            <input type="email" name="email" id="email" required=""
                   :class="{ email , error: !email.valid }"
                   v-model="email.value">
          </div>
          <div>
            <label class="label" for="textarea">Message</label>
            <textarea class="message" name="textarea" id="textarea" required=""
                      v-model="message.text"
                      :maxlength="message.maxlength"></textarea>
            <span class="counter">{{ message.text.length }} / {{ message.maxlength }}</span>
          </div>
          <div>
            <input type="submit" value="Send Form">
          </div>
        </fieldset>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  data: function() {
    return {
      name: "",
      email: {
        value: "",
        valid: true
      },
      message: {
        text: '',
        maxlength: 1000
      },
      submitted: false
    };
  },
  methods: {
    // submit form handler
    submit: function() {
      this.submitted = true;
    },
    // validate by type and value
    validate: function(type, value) {
      if (type === "email") {
        this.email.valid = this.isEmail(value) ? true : false;
      }
    },
    // check for valid email adress
    isEmail: function(value) {
      return emailRegExp.test(value);
    },
    // check or uncheck all
    checkAll: function(event) {
      this.selection.features = event.target.checked ? this.features : [];
    }
  },
  watch: {
    // watching nested property
    "email.value": function(value) {
      this.validate("email", value);
    }
  }
};

</script>

<style>


</style>
