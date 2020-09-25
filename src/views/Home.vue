<template>
  <div class="home d-flex align-items-center position-relative">
    <div class="doge position-absolute"></div>

    <div class="mx-auto" style="z-index:1000">
      <h1 class="my-5">
        <span class="title">Gabba</span><br />
        <span class="title">Doggy</span><br />
        <span class="title">Daycare</span>
      </h1>
      <div class="container">
        <div class="row">
          <div class="col-12 col-md-6 mx-auto">
            <div v-if="submitted">
              <h2>thanks for your interest, we'll keep you updated</h2>
            </div>
            <form
              name="DoggyDaycareEnquiry"
              method="post"
              id="DoggyDaycareEnquiry"
              action="/success"
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
                  <i class="form-icon fal fa-user"></i>
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
                  /><i class="form-icon fal fa-phone-rotary"></i>
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
                  /><i class="form-icon fal fa-envelope"></i>
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
                    placeholder="Hi, I would like to know..."
                    aria-label="Questions/Comments"
                    name="question"
                    required
                    v-model="enquire.question"
                  ></textarea
                  ><i class="form-icon fal fa-comment-alt-lines"></i>
                </div>
              </div>
              <div class="text-left mt-4">
                <button
                  type="submit"
                  class="btn btn-lg btn-cs"
                  aria-label="Submit"
                >
                  <p class="mb-0">
                    <i class="fa fa-paper-plane mr-1 d-inline"></i> Submit
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
          this.$router.push("404");
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
  background: #edb506;
}

.doge {
  height: 100%;
  max-height: 1000px;
  width: 50vw;
  background-image: url("../assets/doge.jpg");
  background-size: contain;
  background-repeat: no-repeat;
  background-position: bottom right;
  right: 0;
  bottom: 0;
}

input.form-control,
textarea.form-control {
  font-size: 1.75rem;
  background: rgba(255, 255, 255, 0.199);
  border: 1px solid transparent;
  border-bottom: 1px solid white;
  font-variation-settings: "wght" 400;
  color: rgb(32, 30, 30);
  &::placeholder {
    color: rgb(104, 92, 92);
    font-variation-settings: "wght" 300;
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
  background: white;
  box-shadow: 2px 4px rgb(85, 187, 255);
  p {
    text-shadow: 1px 1px rgb(98, 184, 255) !important;
  }
}
</style>
