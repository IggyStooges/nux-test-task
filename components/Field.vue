<template>

  <div class="game" v-if="!isWin">

    <transition-group name="flip-list" tag="div" class="field">
      <button v-for="(field, index) in randomFields"
       :key="field"
       :id="index"
       :class="`field__cell field__cell_${field}`"
       @click="clickForPlay">
        {{ field }}
      </button>
    </transition-group>

  </div>
  <div v-else class="success">
    Поздравляем вы победили!
  </div>

</template>



<script>
  export default {
    data: function () {
      return {
        fields: ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13", "14", "15", ""],
        randomFields: [],
        isWin: false,
      };
    },
    methods: {
      markedEmptyCell(el) { //выделим пустую ячейку другим цветом
        if (el.id === "") {
          el.classList.add("empty");
        }
      },
      shuffle() { //рандомно перемешаем массив
        let x = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13", "14", "15", ""];
        x.sort(function () {
          return 0.5 - Math.random()
        });
        return x;
      },
      arrayIsEqual(arr1, arr2) { // установление эквивалентности 2 массивов
        if (arr1.length !== arr2.length) {
          return false
        };
        for (let i = 0; i < arr1.length; i++) {
          if (arr1[i] !== arr2[i]) {
            return false;
          }
        }
        return true;
      },
      clickForPlay(event) { // перемещение элементов, меняем местами с пустой ячейкойю
        let element = document.getElementById(`${event.target.id}`);
        let index = parseInt(element.id);
        let indexNext = index + 1;
        let indexNextRow = index + 4;
        let indexPrev = index - 1;
        let indexPrevRow = index - 4;

        if (this.randomFields[indexNext] === "" && (index % 4) !== 3) {
          let element = this.randomFields[index];
          this.$parent.step += 1;
          this.randomFields.splice(index, 1, this.randomFields[indexNext]);
          this.randomFields.splice(indexNext, 1, element);
        }

        if (this.randomFields[indexNextRow] === "") {
          let element = this.randomFields[index];
          this.$parent.step += 1;
          this.randomFields.splice(index, 1, this.randomFields[indexNextRow]);
          this.randomFields.splice(indexNextRow, 1, element);
        }
        if (this.randomFields[indexPrev] === "" && (index % 4) !== 0) {
          let element = this.randomFields[index];
          this.$parent.step += 1;
          this.randomFields.splice(index, 1, this.randomFields[indexPrev]);
          this.randomFields.splice(indexPrev, 1, element);
        }
        if (this.randomFields[indexPrevRow] === "") {
          let element = this.randomFields[index];
          this.$parent.step += 1;
          this.randomFields.splice(index, 1, this.randomFields[indexPrevRow]);
          this.randomFields.splice(indexPrevRow, 1, element);
        }
        if (this.arrayIsEqual(this.randomFields, this.fields)) {
          this.isWin = true;
        }
      },
    },
    created() { // заполним массив перемешанными элементами
      this.randomFields = this.shuffle(this.fields);
    }
  };

</script>


<style>
  .field {
    width: 100%;
    display: grid;
    grid-template-columns: 25% 25% 25% 25%;
    grid-template-rows: 25% 25% 25% 25%;
  }

  .field__cell {
    padding: 20% 10%;
    border: 2px solid black;
    background: linear-gradient(to top, #fefcea, #f1da36);
    cursor: pointer;
    text-align: center;
    font-weight: bold;
    font-size: 15px;
    border-radius: 5px;
  }

  .field__cell_ {
    opacity: 0.5;
  }

  .flip-list-move {
    transition: transform 0.5s;
  }

  .success {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    padding-top: 10%;
    border: 2px solid red;
    color: red;
    background-color: rebeccapurple;
    font-size: 50px;
    text-align: center;
  }

</style>
