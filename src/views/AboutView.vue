<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="execute">Execute</button>
  </div>
</template>


<script>

import axios from 'axios';

export default{
  data(){
    return{
      vote:0
    }
  },
  methods: {
    async execute(){
  try {
    const response = await axios.get('/execute'); // Changed from POST to GET
    console.log(response.data);
  } catch (error) {
    console.error("Error:", error);
  }
}

  },
};
</script>