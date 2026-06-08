<template>
  <div>
    <h2>Задание 1.1</h2>

    <input v-model="inputValue" placeholder="Введите число" />
    <br />
    <button @click="analyze">Анализировать</button>

    <div v-if="error" class="error">
      {{ error }}
    </div>

    <div v-if="result" class="result">
      <p>Количество цифр: {{ result.digitCount }}</p>
      <p>Первая цифра: {{ result.firstDigit }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Tasks',
  data() {
    return {
      inputValue: '',
      result: null,
      error: ''
    }
  },
  methods: {
    analyze() {
      this.error  = ''
      this.result = null

      const trimmed = this.inputValue.trim()

      // Проверка: пустая строка или не число
      if (trimmed === '' || isNaN(Number(trimmed))) {
        this.error = 'Ошибка: введённое значение не является числом!'
        return
      }

      // Берём абсолютное значение, убираем знак минус
      const numStr = Math.abs(Number(trimmed)).toString()

      // Убираем точку для подсчёта цифр (для дробных чисел)
      const digitsOnly = numStr.replace('.', '')

      this.result = {
        digitCount: digitsOnly.length,
        firstDigit:  digitsOnly[0]
      }
    }
  }
}
</script>