<template lang="pug">
   tr
      td
         | {{skill.name}}
      td 
         input(
            type="text"
            :value="skill.percents"
         )
      td %
      td
         button(type="button" @click="removeSkill") Удалить
</template>

<script>
export default {
   props: {
      skill: Object
   },
   methods: {
      removeSkill() {
         this.$emit('removeSkill', this.skill.id)
      }
   }
}
</script>
