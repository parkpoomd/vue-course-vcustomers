<template>
  	<div class="details container">
  		<router-link to="/">Back</router-link>
  		<h1 class="page-header">{{customer.firstname}}
  			<span class="pull-right">
          <router-link class="btn btn-warning" v-bind:to="'/edit/'+customer.id">Edit</router-link>
          <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">Delete</button>
        </span>
  		</h1>
  		<ul class="list-group">
		  <li class="list-group-item">{{customer.firstname}} {{customer.lastname}}</li>
		  <li class="list-group-item">{{customer.email}}</li>
		</ul>
  	</div>
</template>

<script>
export default {
  name: 'CustomerDetails',
  data () {
    return {
    	customer: ''
    }
  },
  methods: {
  	getCustomerById(id){
  		this.$http.get('http://localhost:3000/customers?id=' + id)
	        .then(function(response){
	          this.customer = response.body;
	    });
  	},
    deleteCustomer(id){
      this.$http.delete('http://localhost:3000/customers?id=' + id)
          .then(function(response){
            this.$router.push({path: '/', query: {alert: 'Customer Deleted'}});
      });
    }
  },
  created: function(){
  	this.getCustomerById(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>