<template>
  <div>
    <h1>Create</h1>
    <form action="" @submit.prevent="CreateCharacter">
      <div>
        <input v-model="test" type="text">
      </div>
      <button type=submit>Create</button>
    </form>
  </div>
</template>

<script>
import gql from 'graphql-tag'
export default {
  name: "CreateCharacter",
  data() {
    return {
      test: ''
    }
  },
  methods: {
    CreateCharacter() {
      this.$apollo.mutate({
        mutation: gql`
          mutation(
            $test: String,
          ){
          createTest(
            input:{
              data:{
                test: $test
              }
            })
            {
              test{
                id
                test
              }}
            }
        `,
        variables: {
          test: this.test
        }
      })
      .then((data) => {
        event.target.reset()
      })
    }
  }
};
</script>
