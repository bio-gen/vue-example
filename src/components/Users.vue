<template>
  <div class="users">
    <h1>Users</h1>

    <div class="well">
      <form v-on:submit="addUser" class="form-inline">
        <div class="form-group">
          <input type="text" v-model="newUser.name" placeholder="Enter Name" class="form-control input-sm">
        </div>
        <div class="form-group">
          <input type="text" v-model="newUser.email" placeholder="Enter E-mail" class="form-control input-sm">
        </div>
        <div class="form-group">
          <input type="submit" value="Add New User" class="btn btn-default btn-sm">
        </div>
      </form>
    </div>

    <table class="table table-striped table-hover table-condensed">
      <thead>
        <tr>
          <th>#</th>
          <th>Name</th>
          <th>E-mail</th>
          <th></th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users">
          <td></td>
          <td><router-link :to="{name: 'UserProfile', params:{id: user.id}}">{{ user.name }}</router-link></td>
          <td><span :class="{contacted: user.contacted}">{{ user.email }}</span></td>
          <td><input type="checkbox" class="toggle" v-model="user.contacted"></td>
          <td>
            <button v-on:click="deleteUser(user)" class="btn btn-danger btn-xs"><i class="glyphicon glyphicon-trash"></i></button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'users',

    data() {
      return {
        newUser: {},
        users: [],
      };
    },

    methods: {
      addUser: function(e) {
        this.users.push({
          name: this.newUser.name,
          email: this.newUser.email,
          contacted: false
        });
        e.preventDefault();
      },

      deleteUser: function(user) {
        this.users.splice(this.users.indexOf(user), 1)
      }
    },

    created: function() {
      this.$http.get('https://jsonplaceholder.typicode.com/users')
        .then(function(response) {
          this.users = response.data;
        });
    }

  }
</script>

<style scoped>
.contacted {
  text-decoration: line-through;
}
</style>