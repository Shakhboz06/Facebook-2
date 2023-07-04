<template>
  <div class="home">
    <h1>Homepage</h1>
    <SearchUser @Search="SearchUser" />
    <br />
    <div v-if="this.FallbackUsers.length" class="page">
      <transition-group name="fade">
        <div v-for="item of FallbackUsers" :key="item.id" class="user">
          <router-link :to="'/user/' + item.id">
            {{ `${item.name} ${item.username}` }}
          </router-link>
          <div class="btns">
            <button @click="deleteItem(item.id)">Delete</button>
            <button @click="editItem(item)">Edit</button>
          </div>
        </div>
      </transition-group>
      <button @click="AddItem(FallbackUsers)" class="NewUser">
        Добавить нового пользователя
      </button>
    </div>
    <span v-else>Nothing is found </span>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import SearchUser from "@/components/SearchUser";

export default {
  name: "Home",
  data() {
    return {
      FallbackUsers: [],
      // Покажите пользователей на главной странице
      users:
        // При клике на пользователя - открывается страница с информацией о нем - используйте window.location
        [
          {
            id: 1,
            name: "Leanne Graham",
            username: "Bret",
            email: "Sincere@april.biz",
            address: {
              street: "Kulas Light",
              suite: "Apt. 556",
              city: "Gwenborough",
              zipcode: "92998-3874",
              geo: {
                lat: "-37.3159",
                lng: "81.1496",
              },
            },
            phone: "1-770-736-8031 x56442",
            website: "hildegard.org",
            company: {
              name: "Romaguera-Crona",
              catchPhrase: "Multi-layered client-server neural-net",
              bs: "harness real-time e-markets",
            },
          },
          {
            id: 2,
            name: "Ervin Howell",
            username: "Antonette",
            email: "Shanna@melissa.tv",
            address: {
              street: "Victor Plains",
              suite: "Suite 879",
              city: "Wisokyburgh",
              zipcode: "90566-7771",
              geo: {
                lat: "-43.9509",
                lng: "-34.4618",
              },
            },
            phone: "010-692-6593 x09125",
            website: "anastasia.net",
            company: {
              name: "Deckow-Crist",
              catchPhrase: "Proactive didactic contingency",
              bs: "synergize scalable supply-chains",
            },
          },
          {
            id: 3,
            name: "Clementine Bauch",
            username: "Samantha",
            email: "Nathan@yesenia.net",
            address: {
              street: "Douglas Extension",
              suite: "Suite 847",
              city: "McKenziehaven",
              zipcode: "59590-4157",
              geo: {
                lat: "-68.6102",
                lng: "-47.0653",
              },
            },
            phone: "1-463-123-4447",
            website: "ramiro.info",
            company: {
              name: "Romaguera-Jacobson",
              catchPhrase: "Face to face bifurcated interface",
              bs: "e-enable strategic applications",
            },
          },
          {
            id: 4,
            name: "Patricia Lebsack",
            username: "Karianne",
            email: "Julianne.OConner@kory.org",
            address: {
              street: "Hoeger Mall",
              suite: "Apt. 692",
              city: "South Elvis",
              zipcode: "53919-4257",
              geo: {
                lat: "29.4572",
                lng: "-164.2990",
              },
            },
            phone: "493-170-9623 x156",
            website: "kale.biz",
            company: {
              name: "Robel-Corkery",
              catchPhrase: "Multi-tiered zero tolerance productivity",
              bs: "transition cutting-edge web services",
            },
          },
          {
            id: 5,
            name: "Chelsey Dietrich",
            username: "Kamren",
            email: "Lucio_Hettinger@annie.ca",
            address: {
              street: "Skiles Walks",
              suite: "Suite 351",
              city: "Roscoeview",
              zipcode: "33263",
              geo: {
                lat: "-31.8129",
                lng: "62.5342",
              },
            },
            phone: "(254)954-1289",
            website: "demarco.info",
            company: {
              name: "Keebler LLC",
              catchPhrase: "User-centric fault-tolerant solution",
              bs: "revolutionize end-to-end systems",
            },
          },
          {
            id: 6,
            name: "Mrs. Dennis Schulist",
            username: "Leopoldo_Corkery",
            email: "Karley_Dach@jasper.info",
            address: {
              street: "Norberto Crossing",
              suite: "Apt. 950",
              city: "South Christy",
              zipcode: "23505-1337",
              geo: {
                lat: "-71.4197",
                lng: "71.7478",
              },
            },
            phone: "1-477-935-8478 x6430",
            website: "ola.org",
            company: {
              name: "Considine-Lockman",
              catchPhrase: "Synchronised bottom-line interface",
              bs: "e-enable innovative applications",
            },
          },
          {
            id: 7,
            name: "Kurtis Weissnat",
            username: "Elwyn.Skiles",
            email: "Telly.Hoeger@billy.biz",
            address: {
              street: "Rex Trail",
              suite: "Suite 280",
              city: "Howemouth",
              zipcode: "58804-1099",
              geo: {
                lat: "24.8918",
                lng: "21.8984",
              },
            },
            phone: "210.067.6132",
            website: "elvis.io",
            company: {
              name: "Johns Group",
              catchPhrase: "Configurable multimedia task-force",
              bs: "generate enterprise e-tailers",
            },
          },
          {
            id: 8,
            name: "Nicholas Runolfsdottir V",
            username: "Maxime_Nienow",
            email: "Sherwood@rosamond.me",
            address: {
              street: "Ellsworth Summit",
              suite: "Suite 729",
              city: "Aliyaview",
              zipcode: "45169",
              geo: {
                lat: "-14.3990",
                lng: "-120.7677",
              },
            },
            phone: "586.493.6943 x140",
            website: "jacynthe.com",
            company: {
              name: "Abernathy Group",
              catchPhrase: "Implemented secondary concept",
              bs: "e-enable extensible e-tailers",
            },
          },
          {
            id: 9,
            name: "Glenna Reichert",
            username: "Delphine",
            email: "Chaim_McDermott@dana.io",
            address: {
              street: "Dayna Park",
              suite: "Suite 449",
              city: "Bartholomebury",
              zipcode: "76495-3109",
              geo: {
                lat: "24.6463",
                lng: "-168.8889",
              },
            },
            phone: "(775)976-6794 x41206",
            website: "conrad.com",
            company: {
              name: "Yost and Sons",
              catchPhrase: "Switchable contextually-based project",
              bs: "aggregate real-time technologies",
            },
          },
          {
            id: 10,
            name: "Clementina DuBuque",
            username: "Moriah.Stanton",
            email: "Rey.Padberg@karina.biz",
            address: {
              street: "Kattie Turnpike",
              suite: "Suite 198",
              city: "Lebsackbury",
              zipcode: "31428-2261",
              geo: {
                lat: "-38.2386",
                lng: "57.2232",
              },
            },
            phone: "024-648-3804",
            website: "ambrose.net",
            company: {
              name: "Hoeger LLC",
              catchPhrase: "Centralized empowering task-force",
              bs: "target end-to-end models",
            },
          },
        ],
    };
  },
  mounted() {
    this.FallbackUsers = this.users;
    this.$root.$on("send", (user, id) => {
      let match = this.FallbackUsers.filter((item) => item.id == id)[0];
      match.name = user.NewName;
      match.phone = user.NewPhone;
      match.website = user.NewWebsite;
    });
  },
  methods: {
    SearchUser: function () {
      let value = event.target.value.toLowerCase().trim();
      this.FallbackUsers = this.users.filter((item) =>
        item.name.toLowerCase().trim().includes(value)
      );
    },
    deleteItem: function (id) {
      this.users = this.users.filter((item) => item.id !== id);
      this.FallbackUsers = this.users;
    },
    editItem: function (user) {
      this.$root.$emit("ShowModal", user);
      console.log(this.FallbackUsers);
    },
    AddItem: function (arr) {
      this.$root.$emit("AddModal", arr);
    },
  },
  components: {
    HelloWorld,
    SearchUser,
  },
};
</script>

<style>
.home {
  font-family: "Gilroy";
}
.user {
  display: flex;
  justify-content: space-between;
  grid-gap: 30px;
  border: 2px solid blue;
  border-radius: 10px;
  margin-top: 5px;
  padding: 5px;
  transition: 0.3s ease;
}
.user:hover {
  transform: scale(1.02);
}
.page {
  display: flex;
  grid-gap: 30px;
  flex-direction: column;
  align-items: center;
}
.btns {
  display: flex;
  justify-content: flex-start;
  grid-gap: 5px;
  align-items: flex-start;
}
.btns button {
  font-family: inherit;
  margin: 5px;
  background-color: blue;
  border: 1px solid blue;
  width: 100px;
  height: 35px;
  border-radius: 10px;
  font-weight: 700;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s ease;
}
.NewUser {
  font-family: inherit;
  margin: 5px;
  background-color: blue;
  border: 1px solid blue;
  width: 250px;
  height: 45px;
  border-radius: 10px;
  font-weight: 700;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
}
.page a {
  font-weight: 700;
  text-decoration: none;
  color: #000;
  margin-top: 10px;
  font-size: 20px;
}
</style>