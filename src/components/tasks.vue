<template>
  <div>
    <!-- Задание 1.1 -->
    <h2>Задание 1.1</h2>
    <input v-model="inputValue" placeholder="Введите число" />
    <br />
    <button @click="analyze">Анализировать</button>
    <div v-if="error" class="error">{{ error }}</div>
    <div v-if="result" class="result">
      <p>Количество цифр: {{ result.digitCount }}</p>
      <p>Первая цифра: {{ result.firstDigit }}</p>
    </div>

    <hr class="divider" />

    <!-- Задание 1.2 -->
    <h2>Задание 1.2</h2>
    <input v-model="stringInput" placeholder="Введите строку" />
    <br />
    <button @click="analyzeString">Анализировать</button>
    <div v-if="stringError" class="error">{{ stringError }}</div>
    <div v-if="everySecondChars.length > 0" class="result">
      <p>Каждый второй символ (с конца): <strong>{{ everySecondChars.join('  ') }}</strong></p>
      <p class="hint">Также выведено в консоль браузера (F12)</p>
    </div>

    <hr class="divider" />

    <!-- Задание 1.3 -->
    <h2>Задание 1.3</h2>
    <input
      v-model="arrayInput"
      placeholder="Введите числа через запятую: 1, 2, 3, 4"
      style="width: 300px"
    />
    <br />
    <button @click="analyzeArray">Вычислить</button>
    <div v-if="arrayError" class="error">{{ arrayError }}</div>
    <div v-if="arrayResult !== null" class="result">
      <p>Элементы массива: <strong>[ {{ parsedArray.join(', ') }} ]</strong></p>
      <p>Количество элементов: <strong>{{ parsedArray.length }}</strong></p>
      <p>Сумма квадратов: <strong>{{ arrayResult }}</strong></p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tasks',
  data() {
    return {
      // 1.1
      inputValue: '',
      result: null,
      error: '',
      // 1.2
      stringInput: '',
      everySecondChars: [],
      stringError: '',
      // 1.3
      arrayInput: '',
      parsedArray: [],
      arrayResult: null,
      arrayError: ''
    }
  },
  methods: {
    // 1.1
    analyze() {
      this.error  = ''
      this.result = null
      const trimmed = this.inputValue.trim()
      if (trimmed === '' || isNaN(Number(trimmed))) {
        this.error = 'Ошибка: введённое значение не является числом!'
        return
      }
      const numStr     = Math.abs(Number(trimmed)).toString()
      const digitsOnly = numStr.replace('.', '')
      this.result = {
        digitCount: digitsOnly.length,
        firstDigit: digitsOnly[0]
      }
    },

    // 1.2
    analyzeString() {
      this.stringError      = ''
      this.everySecondChars = []
      const str = this.stringInput
      if (!str) {
        this.stringError = 'Ошибка: строка пуста!'
        return
      }
      const chars = []
      for (let i = str.length - 1; i >= 0; i -= 2) {
        chars.push(str[i])
      }
      this.everySecondChars = chars
      console.log('Задание 1.2 — каждый второй символ (с конца):', chars.join(' '))
    },

    // 1.3
    analyzeArray() {
      this.arrayError  = ''
      this.arrayResult = null
      this.parsedArray = []

      const str = this.arrayInput.trim()
      if (!str) {
        this.arrayError = 'Ошибка: введите хотя бы один элемент!'
        return
      }

      const parts = str.split(',').map(s => s.trim())
      const numbers = []

      for (const part of parts) {
        if (part === '' || isNaN(Number(part))) {
          this.arrayError = `Ошибка: "${part}" — не является числом!`
          return
        }
        numbers.push(Number(part))
      }

      this.parsedArray = numbers
      this.arrayResult = numbers.reduce((sum, val) => sum + val * val, 0)
    }
  }
}
</script>