<template>
  <div class="home d-flex align-items-center">
    <div class="image-wrapper position-fixed">
      <div class="doge position-absolute"></div>
      <div class="doge2 position-absolute"></div>
    </div>

    <div class="container" style="z-index:1000">
      <!-- <h1 class="my-5">
        <span class="title">Gabba</span><br />
        <span class="title">Doggy</span><br />
        <span class="title">Daycare</span>
      </h1> -->
      <div class="col-12 col-md-4 mx-auto">
        <img
          class="logo w-100 my-4"
          src="../assets/gddc-coming-soon.svg"
          alt=""
        />
      </div>

      <div class="col-12 col-sm-8 col-md-6 col-lg-5 mx-auto mb-5 text">
        <p>Leave your details and we'll keep you updated</p>
      </div>

      <div class="container">
        <div class="row">
          <div class="col-12 col-md-6 mx-auto">
            <div v-if="submitted">
              <h2>thanks for your interest, we'll keep you updated :)</h2>
            </div>
            <form
              name="DoggyDaycareEnquiry"
              method="post"
              id="DoggyDaycareEnquiry"
              action="/"
              @submit.prevent="handleSubmit"
              v-if="!submitted"
            >
              <div class="row">
                <div
                  class="col-md-12 form-group"
                  data-aos="flip-up"
                  data-aos-easing="ease-in-out"
                  data-aos-duration="1000"
                  data-aos-delay="0"
                  data-aos-offset="0"
                >
                  <input
                    class="form-control"
                    type="text"
                    aria-label="Your name"
                    placeholder="Name"
                    name="name"
                    required
                    ref="name"
                    v-model="enquire.name"
                  />
                </div>

                <div
                  class="col-md-12 form-group"
                  data-aos="flip-up"
                  data-aos-easing="ease-in-out"
                  data-aos-duration="1000"
                  data-aos-delay="100"
                  data-aos-offset="0"
                >
                  <input
                    class="form-control"
                    type="tel"
                    placeholder="Phone"
                    aria-label="Your phone number"
                    name="number"
                    v-model="enquire.number"
                    required
                  />
                </div>

                <div
                  class="col-md-12 form-group"
                  data-aos="flip-up"
                  data-aos-easing="ease-in-out"
                  data-aos-duration="1000"
                  data-aos-delay="200"
                  data-aos-offset="0"
                >
                  <input
                    class="form-control"
                    type="email"
                    placeholder="Email"
                    aria-label="Your email address"
                    name="email"
                    v-model="enquire.email"
                  />
                </div>

                <div
                  class="col-md-12 form-group g-mb-40"
                  data-aos="flip-up"
                  data-aos-easing="ease-in-out"
                  data-aos-duration="1000"
                  data-aos-delay="300"
                  data-aos-offset="0"
                >
                  <textarea
                    class="form-control"
                    rows="4"
                    placeholder="Hey, I was wondering..."
                    aria-label="Questions/Comments"
                    name="question"
                    required
                    v-model="enquire.question"
                  ></textarea>
                </div>
              </div>
              <div class="text-center mt-4">
                <button
                  type="submit"
                  class="btn btn-lg btn-cs"
                  aria-label="Submit"
                >
                  <p class="mb-0">
                    <i class="fa fa-paper-plane mr-1 d-inline"></i> Send
                  </p>
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import anime from "animejs";
export default {
  name: "Home",
  data() {
    return {
      enquire: {
        name: "",
        number: "",
        email: "",
        question: ""
      },
      submitted: false
    };
  },
  methods: {
    encode(data) {
      return Object.keys(data)
        .map(
          key => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`
        )
        .join("&");
    },
    handleSubmit() {
      fetch("/", {
        method: "POST",
        headers: { "Content-Type": "application/x-www-form-urlencoded" },
        body: this.encode({
          "form-name": "DoggyDaycareEnquiry",
          ...this.enquire
        })
      })
        .then(() => {
          this.submitted = true;
          // this.$router.push("success");
          // console.log('success')
        })
        .catch(() => {
          // this.$router.push("404");
          // console.log('failure')
        });
    }
  }
};
</script>
<style lang="scss">
.home {
  width: 100vw;
  min-height: 100vh;
  background: #ffbf10;
  background-image: linear-gradient(to bottom, rgb(255, 196, 0), orange);
}

.image-wrapper {
  height: 100vh;
  width: 100vw;
  bottom: 0;
}

.doge {
  height: 100%;
  max-height: 1000px;
  width: 50vw;
  background-image: url("../assets/doge-sm.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: bottom left;
  left: 0;
  bottom: 0;
}

.doge2 {
  height: 100%;
  max-height: 1000px;
  width: 50vw;
  background-image: url("../assets/doge2-sm.png");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: bottom right;
  right: 0;
  bottom: 0;
}

.form * {
  font-family: "Robot Mono";
}

.form-group {
  margin-bottom: 0.4rem !important;
}

input.form-control,
textarea.form-control {
  font-size: 1.75rem;
  background: rgba(255, 206, 149, 0.637);
  border: 1px solid transparent;
  border-bottom: 1px solid rgba(0, 0, 0, 0.267);
  font-variation-settings: "wght" 450;
  color: rgb(0, 0, 0);
  &::placeholder {
    color: rgba(0, 0, 0, 0.486);
    font-variation-settings: "wght" 400;
  }
}

input.form-control:-internal-autofill-selected {
  appearance: menulist-button;
  background-color: rgba(232, 240, 254, 0.322) !important;
  background-image: none !important;
  color: -internal-light-dark(black, white) !important;
}

h1 {
  font-family: "encode Sans", sans-serif;
  font-weight: bold;
  text-transform: uppercase;
  font-variation-settings: "wght" 800;
  color: rgb(255, 255, 255);
  text-shadow: 2px 4px rgb(85, 187, 255);
  .title {
    font-size: calc(50px + (70 - 50) * ((100vw - 300px) / (1600 - 300)));
  }
}

.btn.btn-cs {
  // font-family: "encode sans";
  font-size: 1.5rem;
  background: rgb(54, 208, 255);
  color: rgb(244, 250, 255);
  box-shadow: 0px 4px rgb(33, 155, 236);
  // text-transform: uppercase;
  margin-bottom: 4rem;
  padding: 0.75rem 2.5rem;
  &:hover {
    color: rgb(54, 208, 255);
    background: white;
  }
  p {
    text-shadow: 1px 1px rgb(33, 155, 236) !important;
  }
}

.text {
  font-family: Roboto;
  color: white;
  font-size: 1.3rem;
  font-variation-settings: "wght" 600;
}
</style>
