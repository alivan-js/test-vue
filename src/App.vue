<template>
  <div class="wrapper">
    <Header :isMobile="isMobile" @sortItems="sortItems" @addItem="addNewItem"/>
    <main>
      <AddItem v-if="!isMobile"
               @addItem="addNewItem"
      />
      <ItemList :items="items"
                @deleteItem="deleteItem"/>
    </main>
  </div>
  <Modal v-if="modalOpen" @close="closeModal"/>
</template>

<script>

import Header from "@/features/Header";
import AddItem from "@/features/AddItem";
import ItemList from "@/features/ItemList";
import Modal from "@/shared/components/Modal";

export default {
  name: 'App',
  components: {
    AddItem, Header, ItemList, Modal
  },
  mounted() {
    if (screen.width < 480) {
      this.isMobile = true
    }
    if (localStorage.getItem("items")) {
      this.items = JSON.parse(localStorage.getItem("items"))
    }
  },
  watch: {
    items: function (newItems) {
      localStorage.setItem("items", JSON.stringify(newItems));
    }
  },
  data() {
    return {
      items: [
        {
          id: 1,
          title: "Наименование товара1",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 1000,
          imgUrl: ""
        },
        {
          id: 2,
          title: "Наименование товара2",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 50,
          imgUrl: ""
        },
        {
          id: 3,
          title: "Наименование товара3",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 200,
          imgUrl: ""
        },
        {
          id: 4,
          title: "Наименование товара4",
          description: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 1,
          imgUrl: ""
        },
      ],
      isMobile: false,
      modalOpen: false
    }
  },
  methods: {
    deleteItem(id) {
      this.items = this.items.filter(el => el.id !== id)
    },
    addNewItem(value) {
      this.items = [{
        id: this.items.length + 1,
        title: value.title,
        description: value.description,
        price: value.price,
        imgUrl: value.imgUrl
      }, ...this.items]
      this.modalOpen = true
    },
    sortItems(type) {
      switch (type) {
        case "ascendingPrice":
          this.items.sort((a, b) => a.price - b.price)
          break
        case "descendingPrice":
          this.items.sort((a, b) => b.price - a.price)
          break
        case "descendingTitle":
          this.items.sort((a, b) => {
                if (a.title > b.title) {
                  return 1;
                }
                if (a.title < b.title) {
                  return -1;
                }
                return 0;
              }
          )
          break
      }
    },
    closeModal() {
      this.modalOpen = false
    }
  }
}
</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Source+Sans+Pro:ital,wght@0,200;0,300;0,400;0,600;0,700;0,900;1,200;1,300;1,400;1,600;1,700;1,900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&display=swap');

* {
  padding: 0;
  margin: 0;
  border: 0;
}

*, *:before, *:after {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

:focus, :active {
  outline: none;
}

a:focus, a:active {
  outline: none;
}

nav, footer, header, aside {
  display: block;
}

html, body {
  min-height: 100vh;
  width: 100%;
  background: #E5E5E5;
  line-height: 1;
  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 600;
  color: #3F3F3F;
  font-size: 14px;
  -ms-text-size-adjust: 100%;
  -moz-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}

input, button, textarea {
  font-family: inherit;
}

input::-ms-clear {
  display: none;
}

button {
  cursor: pointer;
}

button::-moz-focus-inner {
  padding: 0;
  border: 0;
}

a, a:visited {
  text-decoration: none;
}

a:hover {
  text-decoration: none;
}

ul li {
  list-style: none;
}

img {
  vertical-align: top;
}

h1, h2, h3, h4, h5, h6 {
  font-size: inherit;
  font-weight: 400;
}

.wrapper {
  margin: 0 auto;
  padding: 32px;
  max-width: 1440px;
}

main {
  top: 132px;
  right: 0;
  display: flex;
}

@media (max-width: 480px) {

  .wrapper {
    padding: 4px 0;
  }

  main {
    flex-direction: column;
    align-items: center
  }

}

</style>
