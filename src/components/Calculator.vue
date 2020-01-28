<template>
  <div class="flex-calculator">
    <h1>Расчёт стоимости автомобиля</h1>

    <div class="price-block">
      <div class="title">Базовая комплектация</div>
      <ul>
        <li v-for="item in basicEquipment" :key="item.id">{{ item.title }} ({{ item.price }}р.)</li>
      </ul>
      <div class="cost">
        Стоимость:
        <span class="cost-equipment">{{ costEquipment }}р.</span>
      </div>
    </div>

    <div class="price-block">
      <div class="title">Дополнительные пакеты</div>
      <div class="grid-packages">
        <div class="packages" v-for="item in additionalPackages" :key="item.id">
          <span>{{ item.title }} ({{ item.price }}р.)</span>
          <input type="checkbox" v-model="item.included" />
        </div>
      </div>
      <div class="cost">
        Стоимость:
        <span class="cost-equipment">{{ costPackages }}р.</span>
      </div>
    </div>

    <div class="total-cost">
      Итоговая стоимость:
      <span class="cost-equipment">{{ totalCost }}р.</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data: function() {
    return {
      basicEquipment: [
        { id: 1, title: "Свойство 1", price: 10000 },
        { id: 2, title: "Свойство 2", price: 11000 },
        { id: 3, title: "Свойство 3", price: 12000 },
        { id: 4, title: "Свойство 4", price: 13000 },
        { id: 5, title: "Свойство 5", price: 14000 }
      ],
      additionalPackages: [
        { id: 1, title: "Пакет 1", price: 10000, included: false },
        { id: 2, title: "Пакет 2", price: 12000, included: false },
        { id: 3, title: "Пакет 3", price: 14000, included: false },
        { id: 4, title: "Пакет 4", price: 16000, included: false },
        { id: 5, title: "Пакет 5", price: 18000, included: false },
        { id: 6, title: "Пакет 6", price: 20000, included: false },
        { id: 7, title: "Пакет 7", price: 22000, included: false },
        { id: 8, title: "Пакет 8", price: 24000, included: false },
        { id: 9, title: "Пакет 9", price: 26000, included: false },
        { id: 10, title: "Пакет 10", price: 28000, included: false },
        { id: 11, title: "Пакет 11", price: 30000, included: false },
        { id: 12, title: "Пакет 12", price: 32000, included: false }
      ]
    };
  },
  computed: {
    costEquipment: function() {
      return this.basicEquipment.reduce(
        (sum, current) => sum + current.price,
        0
      );
    },
    costPackages: function() {
      return this.additionalPackages.reduce((sum, current) => {
        if (current.included) {
          return sum + current.price;
        } else {
          return sum;
        }
      }, 0);
    },
    totalCost: function() {
      return this.costEquipment + this.costPackages;
    }
  }
};
</script>

<style scoped lang="scss">
$width-checkbox: 50px;
$height-checkbox: $width-checkbox / 2;
$color: #7e13c5;
.flex-calculator {
  display: flex;
  align-items: center;
  flex-flow: column nowrap;
  font-size: 16px;
}
.price-block {
  border: 1px solid;
  width: 800px;
  margin-bottom: 30px;
}
.title {
  background: $color;
  color: #fff;
  padding: 5px 10px;
  font-size: 1.3em;
}
.cost {
  margin-right: 10px;
  margin-bottom: 20px;
  text-align: right;
}
.cost-equipment {
  border: 1px solid;
  padding: 5px;
  border-radius: 5px;
}
.total-cost {
  font-size: 1.3em;
}
.grid-packages {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-column-gap: 10px;
  padding: 15px;
}
.packages {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-flow: row nowrap;
  padding: 10px 0px;
}

input[type="checkbox"] {
  width: $width-checkbox;
  height: $height-checkbox;
  -webkit-appearance: none;
  -moz-appearance: none;
  background: #c6c6c6;
  outline: none;
  border-radius: 25px;
  transition: 0.5s;
  position: relative;
}
input:checked[type="checkbox"] {
  background: $color;
}
input[type="checkbox"]::before {
  content: "";
  position: absolute;
  width: $width-checkbox / 2;
  height: $height-checkbox;
  border-radius: 50%;
  top: 0;
  left: 0;
  background: #fff;
  transform: scale(0.9);
  transition: 0.5s;
}
input:checked[type="checkbox"]::before {
  left: $width-checkbox / 2;
}
</style>
