<template>
    <div id='calculator'>
        <input class="calcResult" type="text" v-model="result" />
        <table class="keypadTable">
            <tr>
                <td><button @click="inputNumber('7')">７</button></td>
                <td><button @click="inputNumber('8')">８</button></td>
                <td><button @click="inputNumber('9')">９</button></td>
                <td><button @click="calc('/')">➗</button></td>
            </tr>
            <tr>
                <td><button @click="inputNumber('4')">４</button></td>
                <td><button @click="inputNumber('5')">５</button></td>
                <td><button @click="inputNumber('6')">６</button></td>
                <td><button @click="calc('*')">✖️</button></td>
            </tr>
            <tr>
                <td><button @click="inputNumber('1')">１</button></td>
                <td><button @click="inputNumber('2')">２</button></td>
                <td><button @click="inputNumber('3')">３</button></td>
                <td><button @click="calc('-')">➖</button></td>
            </tr>
            <tr>
                <td><button @click="inputNumber('0')">０</button></td>
                <td><button @click="inputNumber('.')">．</button></td>
                <td><button @click="calc('=')">＝</button></td>
                <td><button @click="calc('+')">➕</button></td>
            </tr>
            <tr>
                <td><button @click="clear()">C</button></td>
                <td><button @click="allClear()">AC</button></td>
            </tr>
        </table>
    </div>
</template>

<script>
  var beforeOperator = false; // 結果表示エリアのクリアフラグ
  var result = '0'; // 計算結果
  var operator = ''; // 予約された演算子
  var num = 0; // 一時保存

  export default {
    data() {
      return {
        result: '0',
      }
    },
    methods: {
      /**
       * 結果表示エリアに入力中の数値を表示
       *
       * @param {*} input
       */
      inputNumber: function(input) {
        // 演算子入力直後
        if(beforeOperator) {
          this.result = '';
          beforeOperator = false
        }

        // 0の時は末尾に追加ではなく置き換え
        if(this.result !== '0') {
          this.result = this.result + input
        } else {
          this.result = input
        }

      },
      /**
       * 計算処理
       *
       * @param {*} input
       */
      calc: function(input) {
        // 入力チェック
        this.inputCheck(this.result)

        // 値の一時保存
        if(input !== num) {
          num = this.result
        }

        // 計算処理
        switch(operator) {
          case '+':
            result = parseFloat(result) + parseFloat(num)
            break
          case '-':
            result = parseFloat(result) - parseFloat(num)
            break
          case '*':
            result = parseFloat(result) * parseFloat(num)
            break
          case '/':
            result = parseFloat(result) / parseFloat(num)
            break
        }

        if(operator === '') {
          // 値の一時保存
          result = this.result
        } else {
          // 計算結果の表示
          this.result = result
        }

        // 次回計算時に使用する演算子として保存
        if(input !== '=') {
          operator = input
        }

        beforeOperator = true
      },
      /**
       * 入力値チェック
       *
       * @param {*} input
       */
      inputCheck: function(input) {
        // 数値および書式に合った「-」、「.」を含む値を許容
        if(!String(input).match('^[-]?[0-9]*[.]?[0-9]*$')) {
          console.log(input + 'is bad value') // デバッグ用
          this.result = '0'
        }
      },
      /**
       * 結果表示エリアをクリア
       */
      clear: function() {
        this.result = '0'
      },
      /**
       * 結果表示エリアおよび保存している値、演算子のクリア
       */
      allClear: function() {
        this.result = '0'
        beforeOperator = false;
        operator = '';
        num = 0;
      }
    }
  }

</script>

<style>
.calcResult {
  text-align: right;
}

.keypadTable {
  margin-right: auto;
  margin-left: auto;
}
</style>