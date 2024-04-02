<script setup></script>

<template>
  <nav class="navbar navbar-expand-lg">
    <div class="container">
      <a href="#" class="col-auto navbar-brand ms-2">
        <img class="" src="../assets/images/logo.svg" alt="logo" />
      </a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
        style="border: none"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse hide navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Features</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Pricing</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#"
              >Resources</a
            >
          </li>
          <hr style="color: white" />
        </ul>
        <ul class="navbar-nav bottom-ul me-2 mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Login</a>
          </li>
          <li class="nav-item mx-auto">
            <button
              class="nav-link active cyan-button btn rounded-pill px-md-4 py-md-2 px-5 fw-bold"
              aria-current="page"
              href="#"
              style="color: #fff"
            >
              Sign Up
            </button>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar a:hover {
  color: #000 !important;
  background-color: transparent;
}
.navbar-brand {
  font-size: 2rem;
  font-weight: 700;
}

.nav-link:not(button) {
  margin-right: 0.5rem;
  color: gray !important;
  font-weight: 600;
}
.cyan-button {
  background-color: hsl(180, 66%, 49%);
  /* padding: 0.4rem; */
}
/* .cyan-button:active {
  background-color: hsl(257, 27%, 26%);
} */
.cyan-button:hover {
  background-color: hsl(180, 66%, 39%);
}

@media (max-width: 62rem) {
  .navbar-collapse {
    background-color: hsl(257, 27%, 26%) !important;
    text-align: center;
    border-radius: 0.5rem;
    padding: 2rem;
    margin: 1rem;
  }
  .navbar .nav-link {
    color: #fff !important;
  }
  .bottom-ul .nav-link:not(button) {
    margin-bottom: 0.5rem;
  }
  .navbar a:hover {
    color: hsl(180, 66%, 49%) !important;
  }
  /* .bottom-ul .nav-item button{
  padding-right: 10rem;
} */
}
</style>
