<template>
  <div>
    <h2>Задание 3</h2>
    <div class="converter">
      <div class="form-group">
        <label>Скорость (км/ч)</label>
        <input
          v-model="kmh"
          type="number"
          placeholder="Введите значение в км/ч"
          @input="fromKmh"
        />
      </div>
      <div class="arrow">⇄</div>
      <div class="form-group">
        <label>Скорость (м/с)</label>
        <input
          v-model="ms"
          type="number"
          placeholder="Введите значение в м/с"
          @input="fromMs"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Task3',
  data() {
    return {
      kmh: '',
      ms:  ''
    }
  },
  methods: {
    fromKmh() {
      if (this.kmh === '' || this.kmh === null) { this.ms = ''; return }
      const val = parseFloat(this.kmh)
      if (isNaN(val)) { this.ms = ''; return }
      this.ms = parseFloat((val / 3.6).toFixed(6))
    },
    fromMs() {
      if (this.ms === '' || this.ms === null) { this.kmh = ''; return }
      const val = parseFloat(this.ms)
      if (isNaN(val)) { this.kmh = ''; return }
      this.kmh = parseFloat((val * 3.6).toFixed(6))
    }
  }
}
</script>