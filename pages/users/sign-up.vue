<template>
  <div>
  <v-row>
    <v-col cols="12" md="4">
      <Register @userData="recieve"/> 
    </v-col>


    <v-col cols="12" md="4">
      {{recievedData}}
    </v-col>



    <v-col cols="12" md="4">
      <UserList :submitted-user="recievedData" />
    </v-col>
  </v-row>
  </div>
</template>

<script>
export default {
  name: 'SignUp',
  data() {
    return {
      recievedData: {},
    }
  },
  methods: {
    recieve(userData) {
      console.log('aaaa');
      this.recievedData = userData;
    }
  }
}
</script>