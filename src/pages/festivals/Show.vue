<template>
  <b-col>
    <h2>Show Festival Page</h2>
    <b-button :to="{ name: 'festivals_edit', params: {id: $route.params.id}}" class="float-right" variant="warning">Edit</b-button>
    <p>
        {{ festival.title }}
    </p>
    <p>
        {{ festival.description }}
    </p>
  </b-col>
</template>

<script>
import axios from '@/config'

export default {
  name: "FestivalsShow",
  components: {},
  data(){
      return{
          festival: {}
      }
  },
  mounted(){
      this.getData()
  },
  methods: {
      getData(){
          let token = localStorage.getItem('token')
          axios
               .get(`/festivals/${this.$route.params.id}`,
               {
                   headers: {
                       "Authorization": `Bearer ${token}` 
                   }
               })
               .then(response => {
                   console.log(response.data)
                   this.festival = response.data
               })
               .catch(error => console.log(error))
      }
  }
};
</script>