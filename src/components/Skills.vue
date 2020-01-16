<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input
          type="text"
          placeholder="Enter a skill you have..."
          v-model="skill"
          v-validate="'min:2'"
          name="skill"
        />
        <!-- errors object is created by vee-validate -->
        <!-- errors.first is to display one error at a time for fields -->
        <p class="alert" v-if="errors.has('skill')">
          {{ errors.first('skill') }}
        </p>
      </form>

      <ul>
        <li v-for="(data, index) in skills" :key="index">{{ data.skill }}</li>
      </ul>

      <p>These are the skills that you possess.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      skill: '',
      skills: [{ skill: 'Vue.js' }, { skill: 'React' }]
    };
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then(result => {
        if (result) {
          this.skills.push({ skill: this.skill });
          this.skill = '';
        }
      });
    }
  }
};
</script>

<style scoped>
.holder {
  background: #fff;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}

p {
  text-align: center;
  padding: 30px 0;
  color: gray;
  margin-top: 0;
}

.container {
  box-shadow: 0 0 40px lightgray;
}

input {
  width: 100%;
  border: 0;
  padding: 20px;
  font-size: 1.3rem;
  background-color: #323333;
  color: #687f7f;
}

p.alert {
  background: #fdf2ce;
  font-weight: bold;
  /* Compared to display: inline, the major difference is that display: inline-block allows to set a width and height on the element */
  /* with display: inline-block, the top and bottom margins/paddings are respected, but with display: inline they are not */
  display: inline-block;
  padding: 5px;
  margin-top: -20px;
}
</style>
