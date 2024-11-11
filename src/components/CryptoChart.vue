<template>
  <div class="cryptoChart__container">
    <div class="buttons__position">
      <div class="buttons__container">
        <button class="btn btn__all">ALL</button>
        <button class="btn btn__one-day" @click="fetchChartData('1')">
          1D
        </button>
        <button class="btn btn__one-week" @click="fetchChartData('7')">
          1W
        </button>
        <button class="btn btn__one-year" @click="fetchChartData('360')">
          1Y
        </button>
      </div>
    </div>
    <div class="grafico">
      <canvas ref="cryptoChart"></canvas>
    </div>
  </div>
</template>

<script setup></script>

<style lang="css" scoped>
.cryptoChart__container {
  width: 875px;
  height: 355px;
  width: clamp(300px, 60vw, 875px);
  border-radius: 35px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  padding: 40px 60px;
  background-color: #022213;
  position: relative;
}

.buttons__position {
  position: absolute;
  right: 0;
  top: 0;
  background-color: #011b0f;
  border-radius: 0px 35px 0px 65px;
  width: 50%;
  height: 25%;
}

.buttons__container {
  padding: 20px 30px;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  gap: 25px;
  width: 100%;
  height: 100%;
}

.btn {
  font-size: 24px;
  width: 75px;
  height: 38px;
  background-color: #b0ec69;
  color: #011b0f;
  border: none;
  border-radius: 50px;
}
.btn__all:hover {
  cursor: no-drop;
}

.grafico {
  width: 100%;
  height: 100%;
  padding-top: 15px;
}

canvas {
  width: 100%;
  height: 100%;
}

@media (width <= 1024px) {
  .buttons__position {
    width: 60%;
  }
  .buttons__container {
    padding: 10px 15px;
    gap: 10px;
    align-items: center;
  }
  .btn {
    width: 20%;
    font-size: 1rem;
  }
}
@media (width <= 768px) {
  .buttons__position {
    width: 100%;
    border-radius: 25px 25px 0 0;
  }
  .buttons__container {
    gap: 20px;
    justify-content: center;
  }
  .btn {
    width: 20%;
  }
}
</style>
