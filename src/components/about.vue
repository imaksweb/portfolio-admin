<template lang="pug">
   .about
      skills-list(
         v-for="(skillType, index) in skillsTypes"
         :key="index"
         :skillType="skillType"
         :skills="skills"
      )
</template>

<script>
import {mapActions, mapGetters} from 'vuex';

export default {
   data() {
      return {
         skillsTypes: ['frontend', 'backend', 'workflow']
      }
   },
   computed: {
      ...mapGetters(['skills'])
   },
   methods: {
      ...mapActions(['fetchSkills'])
   },
   created() {
      this.fetchSkills();
   },
   components: {
      skillsList:  require('./skillsList')
   }
}
</script>



