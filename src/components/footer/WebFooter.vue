<template>
  <footer class="web-footer">
    <div class="container border-top border-bottom">
      <div class="row pt-5 pb-3">
        <!-- Logo Section -->
        <div class="col-md-3">
          <a href="#"><img class="brand-name" src="@/assets/images/logo-alt.svg" alt="Logo" /></a>
          <p class="find-us">Find Us:</p>
          <div class="social-icons mb-3">
            <a href="#"><img src="@/assets/images/icons/facebook.svg" alt="Facebook" /></a>
            <a href="#"><img src="@/assets/images/icons/instagram.svg" alt="Instagram" /></a>
            <a href="#"><img src="@/assets/images/icons/youtube.svg" alt="YouTube" /></a>
          </div>
        </div>

        <!-- Navigation Section -->
        <div class="col-md-3">
          <h5 class="fw-bold mb-3" style="color: #e77e23;">Navigation</h5>
          <div class="d-flex nav-links">
            <ul class="list-unstyled me-5">
              <li><a href="#" class="text-decoration-none">Home</a></li>
              <li><a href="#" class="text-decoration-none">Order</a></li>
              <li><a href="#" class="text-decoration-none">About</a></li>
              <li><a href="#" class="text-decoration-none">Blog</a></li>
            </ul>
            <ul class="list-unstyled">
              <li><a href="#" class="text-decoration-none">Contact</a></li>
              <li><a href="#" class="text-decoration-none">Login</a></li>
              <li><a href="#" class="text-decoration-none">Register</a></li>
            </ul>
          </div>
        </div>

        <!-- Contact Section -->
        <div class="col-md-3">
          <h4>Contact</h4>
          <p>
            <img src="@/assets/images/icons/mail.svg" alt="Email" /> Food.now@mail.com
          </p>
          <p>
            <img src="@/assets/images/icons/phone.svg" alt="Phone" /> +62848477102943
          </p>
          <p>
            <img src="@/assets/images/icons/whatsapp.svg" alt="WhatsApp" /> +628184938494
          </p>
        </div>

        <!-- Location Section -->
        <div class="col-md-3">
          <h4>Location</h4>
          <p>
            <img src="@/assets/images/icons/location.svg" alt="Location" /> Kerobokan
          </p>
          <p>
            Jl. Raya Kerobokan Br Taman, Kuta No.98, Kerobokan Kelod, Kec. Kuta Utara, Kabupaten Badung, Bali 80361
          </p>
        </div>
      </div>
    </div>

    <!-- Copyright Section -->
    <div class="copyright text-center">
      <p>
        Copyright © 2022 Foodnow. All Rights Reserved. Powered by PT. Timedoor Indonesia. | 
        <a href="#">Privacy Policy</a>
      </p>
      <p>
        This site is protected by reCAPTCHA and the Google Privacy Policy and Terms of Service apply.
      </p>
    </div>
  </footer>
</template>

<script>
export default {
  name: "WebFooter",
};
</script>

<style scoped>
.web-footer {
  padding: 40px 0;
  color: #333;
  font-size: 14px;
  font-family: Arial, sans-serif;
}

.brand-name {
  width: 200px;
  height: 100px;
  margin-top: -30px;
}

.find-us {
  color: #ff6600;
  font-size: 18px;
}

.social-icons a img {
  width: 24px;
  height: 24px;
  margin-right: 10px;
}

h4 {
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #ff6600;
}

ul {
  list-style: none;
  padding: 0;
}

ul li {
  margin-bottom: 5px;
}

ul li a {
  text-decoration: none;
  color: #333;
}

ul li a:hover {
  text-decoration: underline;
}

.copyright {
  margin-top: 20px;
  font-size: 12px;
  color: #888;
}

.copyright a {
  color: #333;
  text-decoration: none;
}

p img {
  vertical-align: middle;
  margin-right: 10px;
  width: 18px;
  height: 18px;
}

a:hover {
  color: #ff6600;
}

/* Responsiveness */
@media (max-width: 768px) {
  .web-footer .row > div {
    text-align: center;
    margin-bottom: 20px;
  }

  .social-icons {
    justify-content: center;
    display: flex;
  }

  .nav-links {
    justify-content: center;
    text-align: center;
  }

  .nav-links ul {
    margin: 0 auto;
  }
}

@media (max-width: 576px) {
  .brand-name {
    width: 120px;
  }

  .social-icons a img {
    width: 24px;
    height: 24px;
  }
}
</style>

  