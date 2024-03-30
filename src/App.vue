<script setup>
import navbar from "./components/nav.vue";
import { ref, onMounted } from "vue";

const shortUrl = ref("");
const longUrl = ref("");
const isInvalid = ref(false);
const savedUrls = ref(JSON.parse(localStorage.getItem('savedUrls')) || []);
const reversedUrls = ref(savedUrls.value.reverse());

// onMounted(() => {
//   reversedUrls.value = savedUrls.value.reverse();
// })

async function shortenUrl() {
  if (longUrl.value.trim() === "") {
    isInvalid.value = true;
  } else {
    let xhr = new XMLHttpRequest();
    xhr.open("POST", "https://cleanuri.com/api/v1/shorten", true);
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
    xhr.onreadystatechange = function () {
      if (xhr.readyState === XMLHttpRequest.DONE) {
        if (xhr.status === 200) {
          shortUrl.value = JSON.parse(xhr.responseText);
          console.log(shortUrl.value);
          // Save shortUrl and longUrl as separate items
          savedUrls.value.push({ shortUrl: shortUrl.value.result_url, longUrl: longUrl.value });
          localStorage.setItem("savedUrls", JSON.stringify(savedUrls.value));
        } else {
          console.error("Error:", xhr.status);
        }
      }
    };
    xhr.send("url=" + encodeURIComponent(longUrl.value));
    isInvalid.value = false;
  }
}

async function copyUrl(index){
  // const shortUrl = savedUrls.value[index].shortUrl;
  navigator.clipboard.writeText(index);
}

// async function clearItems(){
//   savedUrls.value = [];
//   localStorage.removeItem('savedUrls');
// }

</script>

<template>
  <header>
    <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->
  </header>

  <main class="container" data-bs-theme="dark">
    <div class="top">
      <navbar />
      <img
        class="img-fluid mt-2"
        src="./assets/images/illustration-working.svg"
        alt=""
      />
      <h1 class="fw-bold text-center mt-5">More than just shorter links</h1>
      <p class="text-center">
        Build your brand’s recognition and get detailed insights on how your
        links are performing.
      </p>
      <div class="middle-button d-flex justify-content-center">
        <button class="btn cyan-button rounded-pill px-4 mb-5">
          Get Started
        </button>
      </div>
    </div>
    <div class="middle">
      <div class="bg-shorten card text-bg-auto mb-3" style="max-width: 18rem">
        <img
          src="./assets/images/bg-shorten-mobile.svg"
          class="card-img img-fluid"
          alt="bg-shorten-mobile"
        />
        <div class="card-img-overlay">
          <form action="" class="row p-2" novalidate>
            <input
              class="form-control"
              :class="{ 'is-invalid': isInvalid }"
              v-model="longUrl"
              type="text"
              placeholder="Shorten a link here..."
              required
            />

            <div class="invalid-feedback mb--1">Please add a link</div>
            <button class="btn cyan-button mt-4" @click.prevent="shortenUrl()">
              Shorten It!
            </button>
          </form>
        </div>
      </div>
      <button class="btn btn-danger" v-if="shortUrl.result_url" @click="clearItems()"> Clear</button>
      <li v-for="(url, index) in reversedUrls" :key="index" style="list-style-type: none;">
        <div class="result mb-3" v-if="shortUrl.result_url">
          <div class="card">
            <div class="card-header">{{ url.longUrl }}</div>
            <div class="card-body">
              <p class="card-text">
                {{ url.shortUrl }}
              </p>
              <button class="btn cyan-button col-12" @click="copyUrl(url.shortUrl)">Copy</button>
            </div>
          </div>
        </div>
      </li>
      <div class="statistics mt-5 mb-4 d-flex flex-column align-items-center">
        <h3>Advanced Statistics</h3>
        <p class="text-center" style="max-width: 30rem">
          Track how your links are performing across the web with our advanced
          statistics dashboard.
        </p>
      </div>
      <div class="brand-recognition">
        <div class="circle">
          <img src="./assets/images/icon-brand-recognition.svg" alt="" />
        </div>
        <h4>Brand Recognition</h4>
        <p>
          Boost your brand recognition with each click. Generic links don’t mean
          a thing. Branded links help instil confidence in your content.
        </p>
      </div>
      <div class="detailed-records">
        <div class="circle">
          <img src="./assets/images/icon-detailed-records.svg" alt="" />
        </div>
        <h4>Detailed Records</h4>
        <p>
          Gain insights into who is clicking your links. Knowing when and where
          people engage with your content helps inform better decisions.
        </p>
      </div>
      <div class="fully-customizable">
        <div class="circle">
          <img src="./assets/images/icon-fully-customizable.svg" alt="" />
        </div>
        <h4>Fully Customizable</h4>
        <p>
          Improve brand awareness and content discoverability through
          customizable links, supercharging audience engagement.
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
        <img src="./assets/images/icon-facebook.svg" alt="" />
        <img src="./assets/images/icon-twitter.svg" alt="" />
        <img src="./assets/images/icon-pinterest.svg" alt="" />
        <img src="./assets/images/icon-instagram.svg" alt="" />
      </div>
    </div>
  </main>
  <div class="attribution">Coded by <a href="#">Sushmoy</a>.</div>
</template>

<style scoped>
.boost {
  background-image: url(./assets/images/bg-boost-mobile.svg);
}

.cyan-button {
  background-color: hsl(180, 66%, 49%);
}

.circle {
  background-color: hsl(257, 27%, 26%);
  max-width: fit-content;
  padding: 1rem;
  border-radius: 50%;
  margin-bottom: 2rem;
}
</style>
