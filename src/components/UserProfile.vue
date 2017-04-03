<template>
  <div>
    <div class="loading" v-if="loading"><p class="text-center">Loading...</p></div>
    <div class="page-header">
      <h2>{{ user.name }}'s Profile
        <div class="pull-right">
          <button v-if="editMode" @click="updateUser" class="btn btn-success btn-xs">
            <i class="glyphicon glyphicon-check"></i>
            Save
          </button>
          <button v-if="editMode" @click="editMode = false" class="btn btn-default btn-xs">
            <i class="glyphicon glyphicon-remove"></i>
            Cancel
          </button>
          <button v-else @click="editMode = true" class="btn btn-default btn-xs">
            <i class="glyphicon glyphicon-pencil"></i>
            Edit
          </button>
        </div>
      </h2>
    </div>

    <!-- Profile Info -->
    <div class="row panel panel-default">
      <div class="panel-body">

        <!-- Avatar -->
        <div class="col-md-2">
          <img class="img-circle img-responsive" src="/static/img/user_avatar.png">
        </div>

        <div class="col-md-4">
          <p><label><i class="glyphicon glyphicon-envelope text-muted"></i> E-mail: </label> {{ user.email }}</p>

          <!-- Phone -->
          <div v-if="editMode" class="form-group">
            <input type="text" class="form-control input-sm" v-model="user.phone">
          </div>
          <div v-else>
            <p><label><i class="glyphicon glyphicon-phone text-muted"></i> Phone: </label> {{ user.phone }}</p>
          </div>

          <!-- Website -->
          <div v-if="editMode" class="form-group">
            <input type="text" class="form-control input-sm" v-model="user.website">
          </div>
          <div v-else>
            <p><label><i class="glyphicon glyphicon-globe text-muted"></i> Website: </label><a :href="user.website" target="_blank"> http://www.{{ user.website }}</a></p>
          </div>

          <!-- Company -->
          <p><label><i class="glyphicon glyphicon-briefcase text-muted"></i> Company: </label> {{ user.company.name }}</p>
        </div>
        <div class="col-md-6">
          <p>
            <address>
              {{ user.address.street }}, {{ user.address.suite }} <br />
              {{ user.address.city }}, {{ user.address.zipcode }} <br />

            </address>
          </p>
        </div>

        <button class="btn btn-success btn-sm">
          <i class="glyphicon glyphicon-star"></i>
          Collaborate
        </button>
      </div>
    </div>

    <!-- Educational Background -->
    <div class="row panel panel-primary">
      <div class="panel-heading">
        <h3 class="panel-title">Educational Background</h3>
      </div>
      <div class="panel-body">
        <div v-if="editMode" class="form-group">
          <input type="textarea" class="form-control" rows="10">
        </div>
      </div>
    </div>

    <!-- Professional Experience -->
    <div class="row panel panel-primary">
      <div class="panel-heading">
        <h3 class="panel-title">Professional Experience</h3>
      </div>
      <div class="panel-body">
        <div v-if="editMode" class="form-group">
          <input type="textarea" class="form-control" rows="10">
        </div>
      </div>
    </div>

    <!-- Certificates -->
    <div class="row panel panel-primary">
      <div class="panel-heading">
        <h3 class="panel-title">Certificates</h3>
      </div>
      <div class="panel-body">
        <div v-if="editMode" class="form-group">
          <input type="textarea" class="form-control" rows="10">
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  export default {
    name: 'user-profile',

    data() {
      return {
        loading: false,
        error: null,

        user: null,
        editMode: false
      };
    },

    methods: {
      fetchData: function() {
        this.error = this.user = null;
        this.loading = true;

        this.$http.get('https://jsonplaceholder.typicode.com/users/' + this.$route.params.id)
          .then(function(response) {
            this.loading = false;
            this.user = response.data;
          });
      },
      updateUser: function() {
        this.editMode = false;
      }

    },

    watch: {
      // call the method again if the route changes
      '$route': 'fetchData'
    },

    created: function() {
      this.fetchData();
    }
  }
</script>

<style>

</style>