<script setup>
</script>

<template>
    <nav class="navbar navbar-expand-lg">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Shortly</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="true" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="navbar-collapse collapse hide mt-2" id="navbarSupportedContent" style="">
          <ul class="navbar-nav bg-body-secondary rounded text-center p-4 me-auto mb-2 mb-lg-0 ">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Features</a>
            </li>
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Pricing</a>
            </li>
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Resources</a>
            </li>
            <hr style="color: white;">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Login</a>
            </li>
            <li class="nav-item mx-auto">
              <button class="nav-link active cyan-button btn rounded-pill px-5" aria-current="page" href="#">Sign Up</button>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </template>

<style scoped>
.navbar-brand{
  font-size: 2rem;
  font-weight: 700;
}
.navbar-nav {
  background-color: hsl(257, 27%, 26%) !important;
}
.nav-link{
  margin: 0.5rem;
  color: white !important;
  font-size: 1rem;
  font-weight: 700;
}
.cyan-button{
  background-color: hsl(180, 66%, 49%);
}
</style>