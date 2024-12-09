<template>
  <header class="header">
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg">
      <div class="container">
        <!-- Brand Logo -->
        <a class="navbar-brand" href="#">
          <img src="@/assets/images/logo.svg" alt="Logo" style="padding-left: 25px" />
        </a>
        <!-- Burger Menu for Mobile -->
        <button
          class="navbar-toggler btn btn-outline-light"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon bg-white"></span>
        </button>
        <!-- Navbar Menu -->
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav mx-auto my-2">
            <li class="nav-item">
              <a class="nav-link text-white" href="#">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link text-white" href="#">Order</a>
            </li>
            <li class="nav-item">
              <a class="nav-link text-white" href="#">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link text-white" href="#">Blog</a>
            </li>
            <li class="nav-item">
              <a class="nav-link text-white" href="#">Contact Us</a>
            </li>
          </ul>
          <div class="d-flex justify-content-center align-items-center me-3">
            <a class="btn btn-outline-light me-2" href="#">Login</a>
            <a class="btn btn-warning" href="#">Register</a>
          </div>
        </div>
      </div>
    </nav>

    <!-- Header Content -->
    <div class="header-content text-center">
      <p class="title">Pizza Order</p>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  background-image: url("@/assets/images/hero.png");
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.navbar {
  padding: 30px;
}

.navbar-brand img {
  height: 40px;
}

.nav-link {
  text-align: center;
  font-size: 1.1rem;
  margin-right: 15px;
  color: white !important;
  text-decoration: none;
  transition: color 0.3s;
}

.nav-link:hover {
  color: orange !important;
}

.header-content {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.header-content .title {
  font-size: 80px;
  color: orange;
  font-weight: bold;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
}

/* Responsive */
@media (max-width: 768px) {
  .header-content .title {
    font-size: 40px;
  }
}
</style>
