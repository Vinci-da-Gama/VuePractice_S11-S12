<template>
  <form name="sample-form-with-validation" novalidate @submit.prevent="submitForm">
    <div :class="['form-control', {'invalid' : userNameValidity === 'invalid'}]">
      <label for="user-name">Your Name</label>
      <input id="user-name" name="user-name" type="text" v-model.trim="userName" @blur="validateUserNameInputed" />
      <p class="text-red" v-if="userNameValidity === 'invalid'">
        Pls enter correct user name
      </p>
    </div>
    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <input id="age" name="age" type="number" v-model="userAge" ref="ageInput" />
    </div>
    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select id="referrer" name="referrer" v-model="referrer">
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <input id="interest-news" name="interest" type="checkbox" value="news" v-model="interest" />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input id="interest-tutorials" name="interest" type="checkbox" value="tutorials" v-model="interest" />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input id="interest-nothing" name="interest" type="checkbox" value="nothing" v-model="interest" />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input id="how-video" name="how" type="radio" value="video" v-model="how" />
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input id="how-blogs" name="how" type="radio" value="blogs" v-model="how" />
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input id="how-other" name="how" type="radio" value="other" v-model="how" />
        <label for="how-other">Other</label>
      </div>
    </div>
    <div class="form-control">
      <rating-control v-model="rating"></rating-control>
    </div>
    <div class="form-control">
      <input
        id="confirm-terms"
        name="confirm-terms"
        type="checkbox"
        value="confirm-the-terms"
        v-model="confirm"
      />
      <label for="confirm-terms">Agree Terms...</label>
    </div>
    <div>
      <button>Save Data</button>
    </div>
  </form>
</template>

<script>
  import RatingControl from './RatingControl';
  export default {
    components: {
      RatingControl,
    },
    data() {
      return {
        userName: '',
        userAge: null,
        referrer: 'wom',
        interest: [],
        how: null,
        confirm: false,
        rating: null,
        userNameValidity: 'pending'
      }
    },
    methods: {
      submitForm() {
        console.log('91 -- username: ', this.userName)
        this.userName = '';
        console.log('93 -- user Age: ', this.userAge + 5)
        console.log('94 -- this.$refs.ageInput.value: ', this.$refs.ageInput.value + 5)
        this.userAge = null;
        console.log('96 -- referrer: ', this.referrer)
        this.referrer = 'wom';
        console.log('98 -- interest: ', this.interest)
        this.interest = [];
        console.log('100 -- how: ', this.how)
        this.how = null;
        console.log('102 -- confirm: ', this.confirm)
        this.confirm = false;
        console.log('104 -- rating: ', this.rating)
        this.rating = null;
      },
      validateUserNameInputed() {
        if (this.userName === '') {
          this.userNameValidity = 'invalid';
        } else {
          this.userNameValidity = 'valid';
        }
      }
    },
  }
</script>

<style lang="scss" scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label {
  color: red;
}

.text-red {
  color: red;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>
