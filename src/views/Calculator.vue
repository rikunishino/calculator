<template>
  <div>
    <input class="calcResult" type="text" v-model="result" />

    <table class="keypadTable">
      <tr>
        <td><button v-on:click="setResultArea('7')">７</button></td>
        <td><button v-on:click="setResultArea('8')">８</button></td>
        <td><button v-on:click="setResultArea('9')">９</button></td>
        <td><button v-on:click="setOperator('/')">➗</button></td>
      </tr>
      <tr>
        <td><button v-on:click="setResultArea('4')">４</button></td>
        <td><button v-on:click="setResultArea('5')">５</button></td>
        <td><button v-on:click="setResultArea('6')">６</button></td>
        <td><button v-on:click="setOperator('*')">✖️</button></td>
      </tr>
      <tr>
        <td><button v-on:click="setResultArea('1')">１</button></td>
        <td><button v-on:click="setResultArea('2')">２</button></td>
        <td><button v-on:click="setResultArea('3')">３</button></td>
        <td><button v-on:click="setOperator('-')">➖</button></td>
      </tr>
      <tr>
        <td><button v-on:click="setResultArea('0')">０</button></td>
        <td><button v-on:click="setResultArea('.')">．</button></td>
        <td><button v-on:click="calc()">＝</button></td>
        <td><button v-on:click="setOperator('+')">➕</button></td>
      </tr>
    </table>
    <button v-on:click="clear()">C</button>
    <br>
    <button v-on:click="debugAreaClear()">Debug</button>
    <input type="text" v-model="debugArea" />
  </div>
</template>

<script>
  export default {
    data() {
      return {
        result: '0',
        debugArea: ''
      }
    },
    methods: {
      // 結果表示エリアをクリア
      clear: function() {
        this.result = '0'
      },
      // デバッグエリアをクリア
      debugAreaClear: function() {
        this.debugArea = ''
      },
      // 結果表示エリアに入力中の数値を表示
      setResultArea: function(input) {
        // 0の時は末尾に追加ではなく置き換え
        if(this.result != 0) {
          this.result = this.result + input
        } else {
          this.result = input
        }
        // TODO: 「.」の入力制限

        // TODO: 演算子を入力後は結果表示エリアをリセット
      },
      // TODO: 選択した演算子をセット
      setOperator: function(input) {
        this.debugArea = input
      },
      // TODO: 計算処理
      calc: function() {
        console.log('計算中...');
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