<template>
  <div>
    <section class="cart">
      <div class="cart__product-name">
        <label>Podaj nazwe produktu:</label><br />
        <input type='text' id='productInput' v-model="productName">
      </div>
      <div class="cart__product-quantity">
        <label>Ilość:</label><br />
        <input type='number' id='quantityInput' v-model="productQuantity">
      </div>
      <div class="cart__radio-container">
        <input class="cart__radio cart__radio--packs" type="radio" name="quantity" value="szt" v-model="productType">Sztuki
        <input class="cart__radio cart__radio--weight" type="radio" name="quantity" value="kg" v-model="productType">Waga<br/>
      </div>
      <div class="cart__product-type">
        <label>Kategoria:</label><br />
        <select v-model="selected" class="cart__selected">
          <option v-for="option in options" v-bind:value="option.value" :key="option.value">
            {{ option.text }}
          </option>
        </select>
      </div>
      <button v-on:click="addProduct">Dodaj</button>
    </section>
    <section class="items-list">
      <ul>
        <li v-for="option in options" :key="option">{{option.text}}:
          <ul>
            <li v-for="arr in option.arr" :key="arr">{{arr.addName}} - {{arr.addQuantity}} {{arr.addType}}</li>
          </ul>
          <p>- - -</p>
        </li>
      </ul>
      <div>
        <p>
          <b>Podsumowanie:</b><br/>
          Waga produków: {{this.totalWeight}}<br/>
          Suma produktów: {{this.totalPacks}}<br/>
        </p>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      productName: "",
      productQuantity: 0,
      productType: "",
      selected: "product1",
      totalWeight: 0,
      totalPacks: 0,
      options: [
        {
          text: "Warzywa",
          value: "product1",
          arr: [],
        },
        {
          text: "Owoce",
          value: "product2",
          arr: [],
        },
        {
          text: "Nabiał",
          value: "product3",
          arr: [],
        },
        {
          text: "Pieczywo",
          value: "product4",
          arr: [],
        },
        {
          text: "Artykuły higieniczne",
          value: "product5",
          arr: [],
        },
      ],
    };
  },
  methods: {
    calcWeight(addType, addQuantity) {
      if (addType == "kg") {
        this.totalWeight = this.totalWeight + addQuantity;
      }
    },
    calcPacks(addType, addQuantity) {
      if (addType == "szt") {
        this.totalPacks += addQuantity;
      }
    },
    addProduct() {
      let addName = this.productName;
      let addQuantity = parseInt(this.productQuantity);
      let addType = this.productType;
      for (let i = 0; i < this.options.length; i++) {
        if (this.selected == this.options[i].value) {
          this.options[i].arr.push({
            addName,
            addQuantity,
            addType,
          });
          this.calcWeight(addType, addQuantity);
          this.calcPacks(addType, addQuantity);
        }
      }
      console.log(this.options);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  /* display: inline-block; */
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>