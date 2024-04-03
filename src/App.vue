<script setup>
import navbar from "./components/nav.vue";
import { ref, onMounted, computed } from "vue";

const shortUrl = ref("");
const longUrl = ref("");
const isInvalid = ref(false);
const savedUrls = ref("");
const copied = ref(false);

onMounted(() => {
  savedUrls.value = JSON.parse(localStorage.getItem("savedUrls")) || [];
});

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
          savedUrls.value.unshift({
            shortUrl: shortUrl.value.result_url,
            longUrl: longUrl.value,
          });
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

async function copyUrl(index) {
  // const shortUrl = savedUrls.value[index].shortUrl;
  navigator.clipboard.writeText(index);
  copied.value = index;
}

async function clearItems() {
  savedUrls.value = [];
  localStorage.removeItem("savedUrls");
}
</script>

<template>
  <header></header>
  <navbar />

  <main class="" data-bs-theme="auto">
    <div
      class="top container p-3 d-lg-flex flex-row-reverse"
      style="margin-bottom: 5rem"
    >
      <img
        class="img-fluid mt-2 px-5 col-lg-7"
        src="./assets/images/illustration-working.svg"
        alt="illustration-working"
      />
      <div class="head-text mx-auto px-1" style="padding-right: 5rem">
        <h1
          class="fs-lg-1 fw-bolder text-center text-lg-start mt-5"
          style="font-size: 2.5rem"
        >
          More than just shorter links
        </h1>
        <p class="text-center text-lg-start">
          Build your brand’s recognition and get detailed insights on how your
          links are performing.
        </p>
        <div
          class="centered-button d-flex justify-content-center justify-content-lg-start"
        >
          <button class="btn cyan-button rounded-pill px-4 mb-5 mt-lg-3">
            Get Started
          </button>
        </div>
      </div>
    </div>
    <div class="middle p-3" id="features">
      <div class="container">
        <div
          class="bg-shorten card mb-3"
          style="background-color: #3a3053; margin-top: -5.8rem"
        >
          <img
            src="./assets/images/bg-shorten-mobile.svg"
            class="card-img d-block d-lg-none"
            alt="bg-shorten-mobile"
            style="max-height: 9.3rem"
          />
          <img
            src="./assets/images/bg-shorten-desktop.svg"
            class="card-img d-none d-lg-block"
            alt="bg-shorten-desktop"
            style="max-height: 6.7rem"
          />
          <div class="card-img-overlay p-4">
            <form action="" class="row px-1 mt-lg-2">
              <div class="col-lg-10">
                <input
                  class="form-control"
                  :class="{ 'is-invalid': isInvalid }"
                  v-model="longUrl"
                  type="text"
                  placeholder="Shorten a link here..."
                  required
                />
                <div class="invalid-feedback">Please add a link</div>
              </div>
              <div class="col-lg-2 row mx-auto">
                <button
                  class="btn cyan-button mt-3 mt-lg-0 mb-2"
                  @click.prevent="shortenUrl()"
                  style="height: 2.4rem"
                >
                  Shorten It!
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
      <div class="d-flex justify-content-end container">
        <button
          class="btn cyan-color mb-3"
          v-if="savedUrls.length !== 0"
          @click="clearItems()"
        >
          <i class="fa-solid fa-square-minus"></i>
          <i> Clean</i>
        </button>
      </div>
      <li
        v-for="(url, index) in savedUrls"
        :key="index"
        style="list-style-type: none"
        class="container"
      >
        <div class="result mb-3">
          <div class="card">
            <div class="card-header">{{ url.longUrl }}</div>
            <div class="container">
              <div
                class="card-body row d-lg-flex flex-lg-row justify-content-lg-between"
              >
                <a
                  class="card-text short-url row col-lg-auto"
                  :href="url.shortUrl"
                  target="_blank"
                >
                  {{ url.shortUrl }}
                </a>
                <button
                  class="btn cyan-button col-lg-auto mt-2 mt-lg-0"
                  @click="copyUrl(url.shortUrl)"
                >
                  Copy
                </button>
              </div>
            </div>
          </div>
        </div>
      </li>
      <div
        class="statistics mt-5 mb-5 mb-lg-0 d-flex flex-column align-items-center"
        style="padding-top: 2.5rem"
      >
        <h3 class="fw-bold">Advanced Statistics</h3>
        <p class="text-center" style="max-width: 30rem">
          Track how your links are performing across the web with our advanced
          statistics dashboard.
        </p>
      </div>
      <div
        class="statistics container d-flex flex-column align-items-center flex-lg-row justify-content-lg-evenly"
      >
        <div
          class="brand-recognition card text-center text-lg-start d-flex align-items-center align-items-lg-start"
        >
          <div class="circle ms-lg-3" style="margin-top: -2rem">
            <img
              src="./assets/images/icon-brand-recognition.svg"
              alt="brand-recognition"
            />
          </div>
          <div class="card-body mb-2">
            <h5 class="card-title">Brand Recognition</h5>
            <p class="card-text">
              Boost your brand recognition with each click. Generic links don’t
              mean a thing. Branded links help instil confidence in your
              content.
            </p>
          </div>
        </div>
        <div class="vertical-line"></div>
        <div
          class="detailed-records card text-center text-lg-start d-flex align-items-center align-items-lg-start"
        >
          <div class="circle ms-lg-3" style="margin-top: -2rem">
            <img
              src="./assets/images/icon-detailed-records.svg"
              alt="detailed-records"
            />
          </div>
          <div class="card-body mb-2">
            <h5 class="card-title">Detailed Records</h5>
            <p class="card-text">
              Gain insights into who is clicking your links. Knowing when and
              where people engage with your content helps inform better
              decisions.
            </p>
          </div>
        </div>
        <div class="vertical-line"></div>
        <div
          class="fully-customizable mb-5 mb-lg-0 card text-center text-lg-start d-flex align-items-center align-items-lg-start"
        >
          <div class="circle ms-lg-3" style="margin-top: -2rem">
            <img
              src="./assets/images/icon-fully-customizable.svg"
              alt="fully-customizable"
            />
          </div>
          <div class="card-body mb-2">
            <h5 class="card-title">Fully Customizable</h5>
            <p class="card-text">
              Improve brand awareness and content discoverability through
              customizable links, supercharging audience engagement.
            </p>
          </div>
        </div>
      </div>
    </div>
  </main>
  <div
    class="boost d-flex flex-column align-items-center justify-content-center"
  >
    <h2 class="mt-5">Boost your links today</h2>
    <button class="btn cyan-button rounded-pill px-4 mb-5">Get Started</button>
  </div>
  <div class="bottom" id="resources">
    <div
      class="container text-center text-lg-start d-lg-flex justify-content-lg-between p-lg-5"
    >
      <h2 class="pt-5 pt-lg-3 pe-lg-5 pb-4 fw-bold">
        <a href="#" class="text-light">Shortly</a>
      </h2>
      <div class="features mb-4 p-lg-3">
        <h4 class="ms-lg-1 mb-lg-3">Features</h4>

        <a href=""> Link Shortening </a>
        <a href=""> Branded Links </a>
        <a href=""> Analytics </a>
      </div>
      <div class="resources mb-4 pt-lg-3 pe-lg-3">
        <h4 class="ms-lg-1 mb-lg-3">Resources</h4>

        <a href=""> Blog </a>
        <a href=""> Developers </a>
        <a href=""> Support </a>
      </div>
      <div class="company mb-5 pt-lg-3 pe-lg-3">
        <h4 class="ms-lg-1 mb-lg-3">Company</h4>

        <a href=""> About </a>
        <a href=""> Our Team </a>
        <a href=""> Careers </a>
        <a href=""> Contact </a>
      </div>
      <div class="social-media pt-lg-3">
        <a href="#">
          <i class="fa-brands fa-facebook fa-xl red"></i>
        </a>
        <a href="#">
          <i class="fa-brands fa-twitter fa-xl"></i>
        </a>
        <a href="#">
          <i class="fa-brands fa-pinterest fa-xl"></i>
        </a>
        <a href="#">
          <i class="fa-brands fa-instagram fa-xl"></i>
        </a>
      </div>
    </div>
  </div>
  <footer
    class="attribution text-center text-secondary p-4"
    style="background-color: hsl(260, 8%, 14%)"
  >
    Coded by <a href="https://github.com/SushCod3">Sushmoy</a>.
  </footer>
</template>

<style scoped>
@media (min-width: 992px) {
  .bg-shorten {
    margin-top: -3.8rem !important;
  }
  .vertical-line {
    border: 0.3rem hsl(180, 66%, 49%) solid !important;
    transform: rotate(90deg);
    height: 37rem !important;
  }
  .statistics {
    margin-top: -5rem;
  }
  .statistics .card {
    width: 20rem !important;
    height: 14.5rem;
    z-index: 1000;
  }

  .brand-recognition {
    margin-top: -3rem;
  }
  .detailed-records {
    margin-top: 2rem;
  }
  .fully-customizable {
    margin-top: 5rem;
  }
  /* .bottom{
    display: flex;
    flex-direction: row;
    align-items: start;
    padding: 2rem;
    
  } */
}

.short-url:hover {
  background-color: transparent !important;
  color: hsl(180, 66%, 39%);
}
.statistics .card {
  width: 19rem !important;
  height: 14.5rem;
  z-index: 1000;
}

/* copied function
.copied{
  background-color: hsl(257, 27%, 26%);
}

:style="{ backgroundColor: copiedIndex === index ? 'hsl(257, 27%, 26%)' : 'hsl(180, 66%, 49%)' }" */

/* h1{
  font-size: 2rem;
} */

/* statistics */
.statistics .card-title {
  margin-top: -1rem;
  font-weight: 700;
  margin-bottom: 0.7rem;
}

.statistics p {
  font-size: smaller;
}

.statistics .card {
  padding: 0 1rem;
}

.middle {
  background-color: #f0f1f6;
  /* padding: 4rem; */
}

/* social media */
.social-media a {
  width: max-content;
  display: inline-block !important;
}

/* boost */
.boost {
  background-image: url(./assets/images/bg-boost-desktop.svg);
  background-size: cover;
  background-color: #3a3053;
  color: white;
}
.vertical-line {
  border: 0.3rem hsl(180, 66%, 49%) solid;
  height: 5rem;
}

/* bottom */

.bottom .text-light {
  font-weight: 600;
}
.bottom .text-light:hover {
  color: hsl(180, 66%, 49%) !important;
}
.bottom {
  background-color: hsl(260, 8%, 14%);
}

.bottom h4 {
  font-weight: 600;
  color: #fff;
  font-size: 1rem;
}

.bottom a {
  color: hsl(257, 7%, 63%);
  display: block;
}
.bottom a:hover {
  background-color: transparent;
}
.bottom i {
  margin: 0.6rem;
}

/* colors */

p {
  color: hsl(257, 7%, 63%);
}
.grayish-violet {
  background-color: hsl(255, 11%, 22%);
}
.cyan-color {
  color: hsl(180, 66%, 49%);
}
.cyan-color:hover {
  color: hsl(180, 66%, 39%);
}
.cyan-button {
  background-color: hsl(180, 66%, 49%);
  color: white;
}
.cyan-button:hover {
  background-color: hsl(180, 66%, 39%);
}

.circle {
  background-color: hsl(257, 27%, 26%);
  max-width: fit-content;
  padding: 1rem;
  border-radius: 50%;
  margin-bottom: 2rem;
}
.invalid-feedback {
  margin-bottom: -1rem;
}

/* social media */
.social-media i:hover {
  color: hsl(180, 66%, 49%);
}
a:hover {
  color: hsl(180, 66%, 49%);
}
</style>
