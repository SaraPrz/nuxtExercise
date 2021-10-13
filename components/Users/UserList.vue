<template>
  <div>
{{submittedUser}}
  </div>
</template>

<script>
export default {
  name: 'UserList',
  props: {
    submittedUser : {
      type: Object,
      default: ()=>{}
    }
  },
  data() {
    return {
      
    }
  },
}
</script>