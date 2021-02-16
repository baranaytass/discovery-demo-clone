<template>
  <div class="body">
    <ul>
      <li v-for="machine in machines">
        <div class="my-main-container" style="margin: 24px">
          <div class="my-container">
            <div style="margin: 18px 8px 18px 8px">
              <div class="my-container-title">
                <a href="#" class="details-button" toggle="tooltip"
                  ><i class="fas fa-search" style="margin-right: 4px"></i
                  > {{ machine.id }}</a
                >
                <br />
                <p>{{ machine.name }}</p>
              </div>
              <div class="my-container-body">
                <div
                  class="flex-wrapper"
                  style="margin-top: 20px; margin-bottom: 20px"
                >
                  <div class="single-chart">
                    <svg viewBox="0 0 36 36" class="circular-chart orange">
                      <path
                        class="circle-bg"
                        d="M18 2.0845
                    a 15.9155 15.9155 0 0 1 0 31.831
                    a 15.9155 15.9155 0 0 1 0 -31.831"
                      />
                      <path
                        class="circle"
                        :stroke-dasharray=" machine.oee "
                        d="M18 2.0845
                    a 15.9155 15.9155 0 0 1 0 31.831
                    a 15.9155 15.9155 0 0 1 0 -31.831"
                      />
                      <text x="18" y="20.35" class="percentage">{{ machine.oee[0] }}%</text>
                    </svg>
                  </div>

                  <div class="single-chart">
                    <svg viewBox="0 0 36 36" class="circular-chart green">
                      <path
                        class="circle-bg"
                        d="M18 2.0845
                    a 15.9155 15.9155 0 0 1 0 31.831
                    a 15.9155 15.9155 0 0 1 0 -31.831"
                      />
                      <path
                        class="circle"
                        :stroke-dasharray=" speedRateCalculate(machine.speed) "
                        d="M18 2.0845
                    a 15.9155 15.9155 0 0 1 0 31.831
                    a 15.9155 15.9155 0 0 1 0 -31.831"
                      />
                      <text x="18" y="20.35" class="percentage">{{machine.speed}}</text>
                    </svg>
                  </div>

                  <div class="statistic">
                    <p><i class="fas fa-chart-bar"></i>Reject Rate : %{{machine.rejectRate}}</p>
                    <p><i class="fas fa-chart-bar"></i>Speed Loss : %{{machine.speedLoss}}</p>
                    <p style="color: #cb5a5e">
                      <i class="fas fa-chart-bar"></i>Rod Weight : %{{machine.rodWeight}}
                    </p>
                  </div>
                </div>

                <div class="container-prod">
                  <span>Completed Production</span>
                </div>

                <div style="margin: 24px 24px 6px 24px">
                  <progress
                    class="progress is-small"
                    :value="machine.completedProd"
                    max="100"
                    style="width: 100%"
                  >
                    {{ machine.completedProd }}%
                  </progress>
                  <p
                    style="
                      text-align: right;
                      font: 550 normal normal 14px/1 FontAwesome;
                      margin-top: 12px;
                    "
                  >
                    {{machine.completedProd}}%
                  </p>
                </div>

                <div class="my-progress-bar" v-if="machine.status == 'on production'">
                  <span> On Production</span>
                </div>

                <div style="height: 10px"></div>
              </div>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "ListMachines",
  props: ["machines"],
  methods: {
    speedRateCalculate(speed) {
      return [speed/10 , 100]
    }
  }
};
</script>

<style scoped>
.body {
  background-image: url(../images/background-world-map.gif);
  background-color: rgb(177, 165, 165);
}
li {
  box-sizing: border-box;
  line-height: 1.42857;
  direction: ltr;
  list-style: none;
  display: inline-block;
  margin-right: 0px;
}

.my-main-container {
  width: 360px;
  height: 450px;
  position: relative;
}

.my-container {
  background-color: #f7f7f7;
  position: relative;
  box-shadow: 0 4px 8px 0 rgb(0 0 0 / 20%), 0 6px 20px 0 rgb(0 0 0 / 19%);
}

.my-container-title {
  padding: 12px;
  border-bottom: 1px solid #eee;
  position: relative;
}

.my-container-title p {
  padding: 0;
  margin: 0;
  text-align: right;
  font-size: 18px;
  color: rgb(53, 152, 220);
  text-transform: uppercase;
  font-weight: 700;
}

.details-button {
  background-color: #cb5a5e;
  color: #fff;
  box-shadow: 0 4px 8px 0 rgb(0 0 0 / 20%), 0 6px 20px 0 rgb(0 0 0 / 19%);
  vertical-align: middle;
  display: inline-block;
  text-decoration: none;
  font-weight: 700;
  font-size: 18px;
  padding: 5px 18px 10px;
  border-radius: 1px;
  margin: 12px 0 12px 0px;
}

.flex-wrapper {
  display: flex;
  flex-flow: row nowrap;
}

.single-chart {
  width: 33%;
  justify-content: space-around;
}

.circular-chart {
  display: block;
  margin: 10px auto;
  max-width: 80%;
  max-height: 250px;
}

.circle-bg {
  fill: none;
  stroke: #eee;
  stroke-width: 3.8;
}

.circle {
  fill: none;
  stroke-width: 2.8;
  stroke-linecap: round;
  animation: progress 1s ease-out forwards;
}

@keyframes progress {
  0% {
    stroke-dasharray: 0 100;
  }
}

.circular-chart.orange .circle {
  stroke: #ff9f00;
}

.circular-chart.green .circle {
  stroke: #4cc790;
}

.circular-chart.blue .circle {
  stroke: #3c9ee5;
}

.percentage {
  fill: #666;
  font-family: sans-serif;
  font-size: 0.5em;
  text-anchor: middle;
}

.statistic {
  font-size: 14px;
  color: #26c281;
  font: 550 normal normal 14px/1 FontAwesome;
  line-height: 14px;
  margin-top: 4px;
  text-rendering: auto;
}

.statistic p {
  margin-bottom: 6px;
}

.container-prod span {
  color: #3598dc;
  font-weight: 700;
  font-family: "Open Sans", sans-serif;
  font-size: 13px;
}

.my-progress-bar {
  margin-bottom: 10px;
  padding: 10px;
  box-shadow: 0 4px 8px 0 rgb(0 0 0 / 20%), 0 6px 20px 0 rgb(0 0 0 / 19%);
  border-color: #228b22 !important;
  background-color: #228b22 !important;
  color: #ffffff !important;
}

.my-progress-bar span {
  font-size: 18px;
  font-family: sans-serif;
}
</style>