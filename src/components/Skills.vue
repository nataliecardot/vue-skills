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

        <!-- Custom animations prefixed by alert-in class are being overridden by imported Animate.css animations flipInX and flipOutX -->
        <transition
          name="alert-in"
          enter-active-class="animated flipInX"
          leave-active-class="animated flipOutX"
        >
          <!-- errors object is created by vee-validate -->
          <!-- errors.first is to display one error at a time for fields -->
          <p class="alert" v-if="errors.has('skill')">
            {{ errors.first('skill') }}
          </p>
        </transition>
      </form>

      <ul>
        <transition-group
          name="list"
          enter-active-class="animated bounceInUp"
          leave-active-class="animated bounceOutDown"
        >
          <!-- To give Vue a hint so that it can track each node’s identity, and thus reuse and reorder existing elements, you need to provide a unique key attribute for each item -->
          <!-- It's bad practice to use an index as a key since arrays are mutable, and the index of any given item can and will change if items are added to or removed from the array; using uuidv4 to generate random string -->
          <li v-for="(item, index) in skills" :key="item.uuid">
            {{ item.skill }}
            <i class="far fa-trash-alt" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul>

      <p>These are the skills that you possess.</p>
    </div>
  </div>
</template>

<script>
import { uuid } from 'vue-uuid';

export default {
  name: 'Skills',
  data() {
    return {
      skill: '',
      skills: [
        { uuid: uuid.v4(), skill: 'Vue' },
        { uuid: uuid.v4(), skill: 'React' },
        { uuid: uuid.v4(), skill: 'Node.js' }
      ]
    };
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then(result => {
        if (result) {
          this.skills.push({ uuid: uuid.v4(), skill: this.skill });
          this.skill = '';
        }
      });
    },
    remove(id) {
      this.skills.splice(id, 1);
    }
  }
};
</script>

<style scoped>
@import 'https://cdn.jsdelivr.net/npm/animate.css@3.5.1';
/* @import "https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css"; */

.holder {
  background: #fff;
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

ul li {
  padding: 1.3rem;
  font-size: 1.3rem;
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}

p {
  text-align: center;
  padding: 2rem 0;
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

.alert-in-enter-active {
  animation: bounce-in 0.5s;
}

.alert-in-leave-active {
  animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

i {
  float: right;
  color: #616161;
  cursor: pointer;
}
</style>
