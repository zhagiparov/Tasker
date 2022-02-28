<template>

  <div class="wrapper">
    <div class="table-time-nav">
      <h3 id="monthAndYear" class="width" onclick="showCalendar()"></h3>
      <button type="button" name="previous" onclick="previous()">&#60;</button>
      <button type="button" name="next" onclick="next()">&#62;</button>
    </div>

      <table id="calendar">
        <thead id="calendar-head">
        <tr>
            <th>вс</th>
            <th>пн</th>
            <th>вт</th>
            <th>ср</th>
            <th>чт</th>
            <th>пт</th>
            <th>сб</th>
        </tr>
        </thead>

          <tbody id="calendar-body">

          </tbody>
      </table>

  </div>

</template>

<script>

export default {
    head() {
      return {
        script: [
          {
             src: '/js/calendar-final.js',
             body: true,
             async: true,
          }
        ],
      }
    }
  }

</script>

<style scoped>

</style>
