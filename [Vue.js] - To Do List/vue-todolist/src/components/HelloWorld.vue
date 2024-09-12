<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="holder">
      <form @submit.prevent="addSkill">
        <Field 
          type="text" 
          placeholder="Enter a skill you have..." 
          v-model="skill" 
          rules="min:5|required" 
          name="skill" 
        />
        <ErrorMessage name="skill">
          <p>Skill must be at least 5 characters long and required.</p>
        </ErrorMessage>
        <button type="submit">Add Skill</button>
      </form>

      <ul>
        <li v-for="(data, index) in skills" :key="index">{{ index }}. {{ data.skill }}</li>
      </ul>

    </div>
  </div>
</template>

<script>
import { Field, ErrorMessage, defineRule, useForm } from 'vee-validate';
import { required, min } from '@vee-validate/rules';

defineRule('required', required);
defineRule('min', min);

export default {
  name: 'HelloWorld',
  components: {
    Field,
    ErrorMessage
  },
  setup() {
    const { handleSubmit } = useForm();

    return {
      handleSubmit
    }
  },
  data() {
    return {
      msg: 'Yurr',
      skill: '',
      skills: [
        { "skill": "Vue.js" },
        { "skill": "Frontend Developer" },
        { "skill": "Backend Developer" },
      ],
    }
  },
  methods: {
    addSkill() {
      // if (this.skill.length >= 5) {
        this.skills.push({ skill: this.skill });
        this.skill = '';
      }
    }
  // }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.alert {
  background-color: yellow;
  width: 100%;
  height: 30px;
}
</style>
