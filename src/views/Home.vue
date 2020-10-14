<template>
  <div class="home">
    <div class="home-content">
      <img class="mb-3" src="../assets/gddc.svg" alt="" />
      <p>Website Coming Soon...</p>
      <button type="button" class="btn btn-cs" @click="showModal">
        Register
      </button>
    </div>

    <modal v-show="isModalVisible" @close="closeModal">
      <template v-slot:body><Register></Register></template>
    </modal>
  </div>
</template>

<script>
import modal from "@/components/Modal.vue";
import Register from "@/views/Register.vue";
export default {
  components: {
    modal,
    Register
  },
  data() {
    return {
      isModalVisible: true
    };
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    }
  }
};
</script>

<style lang="scss">
.home {
  height: 100%;
  display: grid;
  place-items: center;
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
    background: rgb(255, 228, 76);
  }
  p {
    text-shadow: 1px 1px rgb(11, 116, 187) !important;
  }
}
</style>
