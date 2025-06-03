<template>
  <v-row justify="center" align="center">
    <v-col cols="12">

      <v-data-table
    :headers="headers"
    :items="customers"
    :items-per-page="5"
    class="elevation-1"
    :loading ="loading"
    loading-text="loading please waitt">
  <template v-slot:item.profilePicture="{ item }">
    
    <v-badge
    color="purple"
    content="VIP"
    offset-x="10"
    offset-y="40"
    bordered
    v-if="item.isVip == true">

    <v-avatar size="60"></v-avatar> 
    <v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  :src="item.profilePictue"
></v-img>
  </v-badge>

  <div v-else>
    <v-avatar size="60"></v-avatar> 
    <v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  :src="item.profilePictue"
></v-img>
  </div>

  </template>
  
  </v-data-table>

    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return{
      headers: [
          {
            // text: 'ID',
            // align: 'start',
            // sortable: false,
            // value: 'name',
          },
          { text: 'Photo', value: 'profilePicture' },
          { text: 'Name', value: 'name' },
          { text: 'Enail', value: 'email' },
          { text: 'Phone', value: 'phone' },
          { text: 'Address', value: 'address' },
          { text: 'Age', value: 'age' },  
          { text: 'Status', value: 'isVip' },
        ],
        customers: [],
        loading:true
    };
  },
  methods: {
    getCustomers() {
      this.$axios.get('/customers')
      .then(response => {
        console.log(response.data)
        this.customers = response.data
        this.loading = false
      }) 
      .catch(err =>{
        console.log(err)
      })
    }
  },
  mounted() {
    this.getCustomers()
  }
}
</script>
