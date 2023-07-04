<template>
  <div id="AddModals">
    <transition name="fade">
      <div v-if="AddModal">
        <div class="modal modal-edit">
          <div @click="CloseWindow()" class="close">
            <img src="icons/2561211_circle_x_icon.svg" alt="" />
          </div>
          <h2>Add user</h2>
          <div class="inpField">
            <div>
              <input @keyup="NewName()" type="text" placeholder="name" />
              <input
                @keyup="NewPhone()"
                type="text"
                placeholder="phone number"
              />
            </div>
            <div>
              <input @keyup="NewWebsite()" type="text" placeholder="website" />
              <input @keyup="NewStreet()" type="text" placeholder="street" />
            </div>
          </div>
          <div class="elements">
            <h3>{{ Updated.name }}</h3>
            <span>{{ Updated.phone }}</span>
            <p>{{ Updated.website }}</p>
            <p>{{ Updated.username }}</p>
          </div>
          <div class="btns">
            <button @click="Save()">Save</button>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "AddModal",
  data() {
    return {
      AddModal: false,
      Updated: {
        id: Math.random(),
        name: "",
        phone: "",
        website: "",
        username: "",
      },
    };
  },
  mounted() {
    this.$root.$on("AddModal", (arr) => {
      this.AddModal = !this.AddModal;
      arr.push(this.Updated);
    });
  },
  methods: {
    CloseWindow: function () {
      this.AddModal = false;
    },
    Save: function () {
      this.AddModal = false;
    },
    NewName: function () {
      this.Updated.name = event.target.value;
    },
    NewPhone: function () {
      this.Updated.phone = event.target.value;
    },
    NewWebsite: function () {
      this.Updated.website = event.target.value;
    },
    NewStreet: function () {
      this.Updated.username = event.target.value;
    },
  },
};
</script>

<style>
.modal {
  position: absolute;
  left: 50%;
  top: 50%;
  background: #fff;
  padding: 24px;
  border-radius: 24px;
  transform: translate(-50%, -50%);
  border: 3px solid blue;
  font-family: "Gilroy";
}
.modal .inpField {
  display: flex;
  justify-content: center;
  align-items: center;
  grid-gap: 30px;
}
.modal .inpField input {
  width: 250px;
  height: 30px;
  border: 2px solid blue;
  border-radius: 10px;
  font-size: 16px;
  font-weight: 700;
  padding: 5px;
  font-family: inherit;
  margin-top: 15px;
}
.modal .btns {
  display: flex;
  justify-content: center;
  align-items: center;
  grid-gap: 20px;
}
.modal .btns button {
  width: 150px;
  height: 35px;
  border-radius: 10px;
  font-family: inherit;
  font-size: 16px;
  background-color: blue;
  border: 1px solid blue;
  font-weight: 700;
  color: #fff;
}
.modal .close {
  position: absolute;
  right: 24px;
  top: 24px;
  cursor: pointer;
}
.modal .elements p {
  font-weight: 600;
}
.modal .elements span {
  font-weight: 500;
}
.modal h2 {
  margin-top: 0;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>