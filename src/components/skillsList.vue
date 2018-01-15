<template lang="pug">
   div
      .title {{skillType}}
      table.table
         skill-item(
            v-for="skill in skills"
            :key="skill.id"
            :skill="skill"
            v-if="checkSkillType(skillType) === skill.type"
            @removeSkill="removeSkill"
         )
      .addButton
         button(
            type="button"
            @click="addSkill"
         ) Добавить новый
         input(type="text" v-model="newSkill" @keydown.enter="addSkill"
         :class="{error: validation.hasError('newSkill')}"
         )
         div {{validation.firstError('newSkill')}}
</template>

<script>
import{mapMutations} from 'vuex';
import {Validator} from 'simple-vue-validator';
export default {
   mixins: [require('simple-vue-validator').mixin],
   validators: {
      newSkill(value) {
            return Validator.value(value).required('Поле должно быть заполнено')
      }
   },
   props: {
      skillType: String,
      skills: Array
   },
   data() {
      return {
         newSkill: ""
      };
   },
   methods: {
      ...mapMutations(['addNewSkill', 'removeExistedSkill']),
      checkSkillType(skillType) {
         switch(skillType) {
            case 'frontend':
               return 1;
            case "workflow":
               return 2;
            case "backend":
               return 3;
         }
      },
      addSkill() {
         this.$validate().then(success => {
            if(!success) return

            this.addNewSkill({
               id: Math.round(Math.random() * 10000),
               name: this.newSkill,
               percents: 0,
               type: this.checkSkillType(this.skillType)
         });
         this.newSkill = '';
         this.validation.reset();
         });
      },
      removeSkill(skillID) {
         this.removeExistedSkill(skillID)
      }
   },
   components: {
      skillItem: require('./skillsItem')
   }
}
</script>

<style src="styles/skillsList.scss" lang="scss" scoped></style>

