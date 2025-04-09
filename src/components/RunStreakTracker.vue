<template>
  <div>
    <h2>Run Streak Tracker</h2>
    <p>
      Total Days: <span>{{ totalDays }}</span>
    </p>
    <p>
      Total Weeks: <span>{{ totalWeeks }}</span>
    </p>
    <p>
      Total Months: <span>{{ totalMonths }}</span>
    </p>
    <p>
      Total Years: <span>{{ totalYears }}</span>
    </p>
    <h3>Milestones</h3>
    <p>
      <span>{{ daysToNextMilestone }}</span> days until <span>{{ nextDayMilestone }}</span> days of
      running
    </p>
    <p>
      <span>{{ daysToNextWeekMilestone }}</span> days until
      <span>{{ nextWeekMilestone }}</span> weeks of running
    </p>
    <p>
      <span>{{ daysToNextMonthMilestone }}</span> days until
      <span>{{ nextMonthMilestone }}</span> months of running
    </p>
    <p>
      <span>{{ daysToNextYearMilestone }}</span> days until
      <span>{{ nextYearMilestone }}</span> years of running
    </p>
    <h3>Facts (at 5k/day)</h3>
    <p>
      Runs around the Earth: <span>{{ timesAroundEarth }}</span>
    </p>
    <p>
      Runs across the USA: <span>{{ timesAcrossUSA }}</span>
    </p>
    <p>
      Salmon Mains run: <span>{{ salmonMainsRun }}</span>
    </p>
    <p>
      Lake Shore Trails: <span>{{ lakeShoreTrails }}</span>
    </p>
    <p>
      Laps around Cedar Point: <span>{{ lapsAroundCedarPoint }}</span>
    </p>
    <p>
      Time spent running: <span>{{ timeSpentRunning }}</span>
    </p>
    <p>
      Shoes worn out: <span>{{ shoesWornOut }}</span>
    </p>
    <p>
      Calories burned: <span>{{ caloriesBurned }}</span>
    </p>
    <p>
      Total steps taken: <span>{{ totalSteps }}</span>
    </p>
  </div>
</template>

<script setup>
import { computed } from "vue"

const startDate = new Date("2012-02-01")
const currentDate = new Date()

const totalDays = computed(() => {
  const diffTime = Math.abs(currentDate - startDate)
  return Math.ceil(diffTime / (1000 * 60 * 60 * 24))
})

const totalWeeks = computed(() => {
  return Math.floor(totalDays.value / 7)
})

const totalMonths = computed(() => {
  return Math.floor(totalDays.value / 30)
})

const totalYears = computed(() => {
  return Math.floor(totalDays.value / 365)
})

const nextDayMilestone = computed(() => {
  return Math.ceil(totalDays.value / 500) * 500
})

const daysToNextMilestone = computed(() => {
  return nextDayMilestone.value - totalDays.value
})

const nextWeekMilestone = computed(() => {
  return Math.ceil(totalWeeks.value / 100) * 100
})

const daysToNextWeekMilestone = computed(() => {
  return nextWeekMilestone.value * 7 - totalDays.value
})

const nextMonthMilestone = computed(() => {
  return Math.ceil(totalMonths.value / 50) * 50
})

const daysToNextMonthMilestone = computed(() => {
  return nextMonthMilestone.value * 30 - totalDays.value
})

const nextYearMilestone = computed(() => {
  return Math.ceil(totalYears.value + 1)
})

const daysToNextYearMilestone = computed(() => {
  return nextYearMilestone.value * 365 - totalDays.value
})

// Facts calculations
const kmPerDay = 5
const minutesPerDay = 30
const caloriesPerRun = 310
const milesPerKm = 0.621371
const milesPerShoe = 400
const stepsPerRun = 6220

const timesAroundEarth = computed(() => {
  return ((totalDays.value * kmPerDay) / 40075).toFixed(4)
})

const timesAcrossUSA = computed(() => {
  return ((totalDays.value * kmPerDay) / 4654).toFixed(3)
})

const lapsAroundCedarPoint = computed(() => {
  return ((totalDays.value * kmPerDay * milesPerKm) / 4.1).toFixed(2)
})

const lakeShoreTrails = computed(() => {
  return ((totalDays.value * kmPerDay * milesPerKm) / 18).toFixed(2)
})

const salmonMainsRun = computed(() => {
  return ((totalDays.value * kmPerDay * milesPerKm) / 82).toFixed(2)
})

const shoesWornOut = computed(() => {
  return ((totalDays.value * kmPerDay * milesPerKm) / milesPerShoe).toFixed(2)
})

const caloriesBurned = computed(() => {
  return (totalDays.value * caloriesPerRun).toLocaleString()
})

const totalSteps = computed(() => {
  return (totalDays.value * stepsPerRun).toLocaleString()
})

const timeSpentRunning = computed(() => {
  const totalMinutes = totalDays.value * minutesPerDay
  const days = Math.floor(totalMinutes / (24 * 60))
  const hours = Math.floor((totalMinutes % (24 * 60)) / 60)
  return `${days} days, ${hours} hours`
})
</script>

<style scoped>
div {
  text-align: center;
  margin-top: 20px;
  font-family: Arial, sans-serif;
}

h2 {
  color: #2c3e50;
  margin-bottom: 20px;
}

p {
  margin: 10px 0;
  font-size: 1.2em;
}

p span {
  font-weight: bold;
  color: #42b983;
}

h3 {
  margin-top: 30px;
  color: #34495e;
}
</style>
