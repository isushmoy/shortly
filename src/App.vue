<script setup>
import navbar from './components/nav.vue'

</script>

<template>
  <header>
    <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->
  </header>

  <main class="container">
    <div class="top">
      <h1 class="text-4xl font-bold">Shortly</h1>
      <nav>
        <navbar />
        Features Pricing Resources
        <hr />
        Login Sign Up
      </nav>
      <img src="./assets/images/illustration-working.svg" alt="" />

      <h1>More than just shorter links</h1>
      <p>
        Build your brand’s recognition and get detailed insights on how your
        links are performing.
      </p>
      <button>Get Started</button>
    </div>
    <div class="middle">
      <div class="bg-shorten">
        <form action="">
          <input type="text" placeholder="Shorten a link here..." />
          <button>Shorten It!</button>
        </form>
      </div>
      <h3>Advanced Statistics</h3>
      <p>
        Track how your links are performing across the web with our advanced
        statistics dashboard.
      </p>
      <div class="brand-recognition">
        <img src="./assets/images/icon-brand-recognition.svg" alt="">
        <h4>Brand Recognition</h4>
        <p>
          Boost your brand recognition with each click. Generic links don’t mean a
          thing. Branded links help instil confidence in your content.
        </p>
      </div>
      <div class="detailed-records">
        <img src="./assets/images/icon-detailed-records.svg" alt="">
        <h4>Detailed Records</h4>
        <p>
          Gain insights into who is clicking your links. Knowing when and where
          people engage with your content helps inform better decisions.
        </p>
      </div>
      <div class="fully-customizable">
        <img src="./assets/images/icon-fully-customizable.svg" alt="">
        <h4>Fully Customizable</h4>
        <p>
          Improve brand awareness and content discoverability through customizable
          links, supercharging audience engagement.
        </p>
      </div>
    </div>
    <div class="boost">
      <h2>Boost your links today</h2>
      <button>Get Started</button>
    </div>

    <div class="bottom">
      <h2>Shortly</h2>

      <h4 href="">Features</h4>

      <a href=""> Link Shortening </a>
      <a href=""> Branded Links </a>
      <a href=""> Analytics </a>

      <h4>Resources</h4>

      <a href=""> Blog </a>
      <a href=""> Developers </a>
      <a href=""> Support </a>

      <h4>Company</h4>

      <a href=""> About </a>
      <a href=""> Our Team </a>
      <a href=""> Careers </a>
      <a href=""> Contact </a>
      <div class="social-media">
        <img src="./assets/images/icon-facebook.svg" alt="">
        <img src="./assets/images/icon-twitter.svg" alt="">
        <img src="./assets/images/icon-pinterest.svg" alt="">
        <img src="./assets/images/icon-instagram.svg" alt="">
      </div>
    </div>
  </main>
  <div class="attribution">
    Coded by <a href="#">Sushmoy</a>.
  </div>
</template>

<style scoped>
.boost {
  background-image: url(./assets/images/bg-boost-mobile.svg);
}
.bg-shorten{
  background-image: url(./assets/images/bg-shorten-mobile.svg);
}

</style>
