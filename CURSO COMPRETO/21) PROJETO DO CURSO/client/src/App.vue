<template>
  <div id="app">
    <!-- BEGIN NAVBAR -->
    <nav class="navbar navbar-expand-lg bg-dark navbar-dark">
      <div class="container-fluid">
        <a class="navbar-brand">Full Stack App - Azure SQL + Prisma</a>

        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/"
              >Create New Employee</router-link
            >
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/list-employees"
              >List All Employees</router-link
            >
          </li>
        </ul>
      </div>
    </nav>
    <!-- END NAVBAR -->

    <div class="container mt-5">
      <router-view></router-view>
    </div>
  </div>
</template>
