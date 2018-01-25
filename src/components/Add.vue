<template>
  	<div class="add container">
  		<h1 class="page-header">Add Customer</h1>
      <Alert v-if="alert" v-bind:message="alert" />
  		<form v-on:submit="addCustomer">
  			<div class="well">
  				<h4>Customer Info</h4>
  				<div class="form-group">
  					<label>First Name</label>
  					<input type="text" class="form-control" placeholder="First Name" v-model="customer.firstname">
  				</div>
  				<div class="form-group">
  					<label>Last Name</label>
  					<input type="text" class="form-control" placeholder="Last Name" v-model="customer.lastname">
  				</div>
  				<div class="form-group">
  					<label>Email</label>
  					<input type="text" class="form-control" placeholder="Email" v-model="customer.email">
  				</div>
  			</div>
  			<button type="submit" class="btn btn-primary">Submit</button>
  		</form>
  	</div>
</template>

<script>
import Alert from './Alert'
export default {
  name: 'add',
  data () {
    return {
    	customer: {},
      alert: ''
    }
  },
  methods: {
  	addCustomer(e){
  		if(!this.customer.firstname || !this.customer.lastname || !this.customer.email){
  			this.alert = 'Please fill in all required fields';
  		} else {
  			let newCustomer = {
  				firstname: this.customer.firstname,
  				lastname: this.customer.lastname,
  				email: this.customer.email
  			}

  			this.$http.post('http://localhost:3000/customers', newCustomer)
  				.then(function(response){
  					this.$router.push({path: '/', query: {alert: 'Customer Added'}});
  				});
  			e.preventDefault();
  		}
  		e.preventDefault();
  	}
  },
  components: {
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>