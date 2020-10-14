<template>
  <div class="register d-flex align-items-center position-relative">
    <div class="image-wrapper position-absolute">
      <div class="doge position-absolute"></div>
      <div class="doge2 position-absolute"></div>
    </div>

    <div class="container content-wrapper" style="z-index:1000">
      <!-- <h1 class="my-5">
        <span class="title">Gabba</span><br />
        <span class="title">Doggy</span><br />
        <span class="title">Daycare</span>
      </h1> -->
      <div class="top-part">
        <img class="logo my-4" src="../assets/gddc-coming-soon.svg" alt="" />

        <div class="col-12 col-sm-8 col-md-6 col-lg-5 mx-auto text">
          <p>Leave your details and we'll keep you updated</p>
        </div>
      </div>

      <div class="container bottom-part">
        <div class="row">
          <div class="col-12 col-md-6 mx-auto">
            <div v-if="submitted" class="my-5 thanks-msg">
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
                    v-model="enquire.question"
                  ></textarea>
                </div>
              </div>
              <div class="text-center mt-4">
                <button type="submit" class="btn btn-cs" aria-label="Submit">
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
export default {
  name: "Register",
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
          this.$router.push("404");
          // console.log('failure')
        });
    }
  }
};
</script>
<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Encode+Sans:wdth,wght@87.5,621&family=Roboto+Mono:wght@401&display=swap");

.register {
  font-family: "Roboto Mono", "Courier New", Courier, monospace;
  width: 100%;
  height: 100%;
  background: #ffbf10;
  background-image: linear-gradient(to bottom, rgb(255, 196, 0), orange);
}

.content-wrapper {
  display: grid;
  grid-template-rows: min-max(100px, 300px) auto;
  .top-part {
    width: 100%;
  }
}

.logo {
  width: 100%;
  max-width: 250px;
  margin: auto;
}

.image-wrapper {
  height: 100%;
  width: 100%;
  bottom: 0;
}

.doge {
  height: 100%;
  max-height: 1000px;
  width: 50%;
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
  width: 50%;
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
  font-size: 1.25rem;
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
  // appearance: menulist-button;
  background-color: rgba(254, 244, 232, 0.295) !important;
  background-image: none !important;
  color: -internal-light-dark(black, white) !important;
}

.thanks-msg {
  background: rgba(255, 255, 255, 0.486);
  padding: 10px;
  border-radius: 0.25rem;
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
  // font-size: 1.5rem;
  background: #27aae1;
  color: rgb(255, 255, 255);
  box-shadow: 0px 4px rgb(11, 116, 187);
  // text-transform: uppercase;
  margin-bottom: 2rem;
  padding: 0.75rem 2.5rem;
  &:hover {
    color: #27aae1;
    background: white;
  }
  p {
    text-shadow: 1px 1px rgb(11, 116, 187) !important;
  }
}

.text {
  font-family: Roboto;
  color: white;
  font-size: 1.3rem;
  font-variation-settings: "wght" 600;
}
</style>
