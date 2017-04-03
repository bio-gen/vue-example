<template>
  <div id="app">
    <nav class="navbar navbar-default">
      <div class="container">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <router-link to="/" class="navbar-brand">Healthnetz</router-link>
        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
          <form class="navbar-form navbar-left">
            <div class="form-group">
              <input type="text" class="form-control input-sm" placeholder="Search">
            </div>
            <button type="submit" class="btn btn-default btn-sm">Search</button>
          </form>

          <ul class="nav navbar-nav navbar-right">
            <li>
              <router-link to="/">
                <i class="glyphicon glyphicon-user"></i>
                Profile<span class="sr-only">(current)</span></router-link>
            </li>
            <li>
              <router-link to="/">
                <i class="glyphicon glyphicon-comment"></i>
                Meeting<span class="sr-only">(current)</span></router-link>
            </li>
            <li>
              <router-link to="/">
                <i class="glyphicon glyphicon-envelope"></i>
                Inbox<span class="sr-only">(current)</span></router-link>
            </li>
            <li>
              <router-link to="/">
                <i class="glyphicon glyphicon-bell"></i>
                Notifications<span class="sr-only">(current)</span></router-link>
            </li>
            <li>
              <router-link to="/">
                <i class="glyphicon glyphicon-cog"></i>
                Settings<span class="sr-only">(current)</span></router-link>
            </li>
          </ul>

        </div>
      </div>
    </nav>

    <transition name="fade" mode="out-in">
      <router-view class="view"></router-view>
    </transition>
  </div>
</template>

<script>

import Users from './components/Users'

export default {
  name: 'app',
  components: {
    Users
  }
}
</script>

<style>
</style>
