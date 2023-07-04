<template>
  <div id="modals">
    <transition name="fade">
      <div class="modal modal-edit" v-if="EditModal">
        <div class="close" @click="CloseWindow()">
          <img src="icons/2561211_circle_x_icon.svg" alt="" />
        </div>
        <h2>Edit element</h2>
        <div class="info">
          <input
            @keyup="NewName()"
            :value="Updated.name"
            type="text"
            placeholder="name"
          />
          <input
            @keyup="NewPhone()"
            :value="Updated.phone"
            type="text"
            placeholder="phone number"
          />
          <input
            @keyup="NewWebsite()"
            :value="Updated.website"
            type="text"
            placeholder="website"
          />
        </div>
        <div class="elements">
          <h3>{{Updated.name}}</h3>
          <span>{{Updated.phone}}</span>
          <p>{{Updated.website}}</p>
        </div>
        <div class="btns">
          <button @click="AddNewItem(Updated.id)">Save</button>
          <button @click="Leave()">Go back</button>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      Updated: "",
      Changed: [
        {
          id: Math.random(),
          NewName: "",
          NewPhone: "",
          NewWebsite: "",
        },
      ],
      EditModal: false,
    };
  },
  mounted() {
    this.$root.$on("ShowModal", (user) => {
      this.EditModal = !this.EditModal;
      this.Updated = user;
      this.Changed.NewName = user.name;
      this.Changed.NewPhone = user.phone;
      this.Changed.NewWebsite = user.website;
    });
  },
  methods: {
    CloseWindow: function () {
      this.EditModal = !this.EditModal;
    },
    Leave: function () {
      this.EditModal = !this.EditModal;
    },
    NewName: function () {
      this.Changed.NewName = event.target.value;
    },
    NewPhone: function () {
      this.Changed.NewPhone = event.target.value;
    },
    NewWebsite: function () {
      this.Changed.NewWebsite = event.target.value;
    },
    AddNewItem: function (id) {
      this.EditModal = !this.EditModal;
      this.$root.$emit("send", this.Changed, id);
    },
  },
};
</script>

<style>
.modal {
  position: absolute;
  left: 50%;
  top: 60%;
  background: #fff;
  padding: 24px;
  border-radius: 24px;
  transform: translate(-50%, -50%);
  border: 3px solid blue;
  font-family: "Gilroy";
}
.modal .info input {
  width: 180px;
  height: 30px;
  margin-left: 10px;
  border: 2px solid blue;
  border-radius: 10px;
  font-size: 16px;
  font-weight: 700;
  padding: 5px;
  font-family: inherit;
}
.modal .btns{
  display: flex;
  justify-content: center;
  align-items: center;
  grid-gap: 20px;
}
.modal .btns button{
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
.modal .elements p{
  font-weight: 600;
}
.modal .elements span{
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