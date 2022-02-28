<template>

  <div class="wrapper">
    <div class="table-time-nav">
      <h3 class="width-wider" id="monthAndYear"></h3>
      <button type="button" name="previous" id="previous" @click="prevWeek()">&#60;</button>
      <button type="button" name="next" id="next" @click="nextWeek()">&#62;</button>
    </div>

    <table id="calendar" class="week-table">
        <thead id="calendar-head">

        </thead>

        <tbody id="calendar-body">

        </tbody>
    </table>

  </div>

</template>

<script>

export default {
  data() {
    return {
      shortDayNames: ['вс', 'пн', 'вт', 'ср', 'чт', 'пт', 'сб'],
      monthNames: ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь', 'Июль', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь'],
      shortDayNamesEng: ['su', 'mo', 'tu', 'we', 'th', 'fr', 'sa'],
      monthNamesEng: ['jan', 'feb', 'mar', 'apr', 'may', 'jun', 'jul', 'aug', 'sep', 'oct', 'nov', 'dec'],
      year: 2022, month: 0, day: 3,
      today: null, firstWeekStart: null, currentWeekStart: null, n: 0, difference: 0, daysBetween: 0,
      row: null, hdr: null, tbl: null, k: -1, j: -1,
      thCell: null, thCellDiv: null, thCellTextDay: null, thCellTextDate: null,
      tdCell: null,
      monthsInWeek: [], noDuplicates: [], yearsInWeek: [], noDuplicatesY: [], displayedDate: null,
      dateNameFormat: { year: 'numeric', month: '2-digit', day: '2-digit' },
    }
  },
  mounted: function() {
        setTimeout(() => {
          this.initVars();
        }, 0);
  },
  methods: {
    initVars() {
      this.today = new Date();
      this.firstWeekStart = new Date(this.year, this.month, this.day);
      this.currentWeekStart = new Date(this.year, this.month, this.day);
      this.calculateCurrentPosition();
    },
    prevWeek() {
      this.n--;
      this.currentWeekStart = new Date(this.year, this.month, this.day+(this.n*14));
      this.showWeek();
    },
    nextWeek() {
      this.n++;
      this.currentWeekStart = new Date(this.year, this.month, this.day+(this.n*14));
      this.showWeek();
    },
    removeDuplicates(arr) {
      this.noDuplicates = arr.filter((item, index) => arr.indexOf(item) === index);
    },
    removeDuplicatesY(arr) {
      this.noDuplicatesY = arr.filter((item, index) => arr.indexOf(item) === index);
    },
    calculateCurrentPosition() {
      this.difference = Math.abs(this.today - this.firstWeekStart);
      this.daysBetween = this.difference / (1000 * 3600 * 24);
      this.n = Math.floor(this.daysBetween / 14);
      this.showWeek();
    },
    showWeek() {
      this.monthsInWeek = [];
      this.noDuplicates = [];
      this.yearsInWeek = [];
      this.noDuplicatesY = [];
      this.k = -1;
      this.j = -1;
      this.displayedDate = document.getElementById("monthAndYear");
      this.hdr = document.getElementById("calendar-head");
      this.tbl = document.getElementById("calendar-body");
      this.row = document.createElement("tr");
      this.hdr.innerHTML = "";
      this.displayedDate.innerHTML = "";
      for (let i = 0; i < 14; i++) {
        this.thCell = document.createElement("th");
        this.thCellDiv = document.createElement("span");
        this.thCellDiv2 = document.createElement("span");
        this.thCellTextDate = document.createTextNode((new Date(this.year, this.month, this.day+(this.n*14)+i)).getDate());
        if (this.currentWeekStart.getDay()+i > 6 && this.currentWeekStart.getDay()+this.k > 6) {
          this.thCellTextDay = document.createTextNode(this.shortDayNames[this.currentWeekStart.getDay()+this.j]);
          this.j++;
        } else if (this.currentWeekStart.getDay()+i > 6) {
          this.thCellTextDay = document.createTextNode(this.shortDayNames[this.currentWeekStart.getDay()+this.k]);
          this.k++;
        } else {
          this.thCellTextDay = document.createTextNode(this.shortDayNames[this.currentWeekStart.getDay()+i]);
        }
        if ((new Date(this.year, this.month, this.day+(this.n*14)+i)).getDate() === this.today.getDate()
        && (new Date(this.year, this.month, this.day+(this.n*14)+i)).getFullYear() === this.today.getFullYear()
        && (new Date(this.year, this.month, this.day+(this.n*14)+i)).getMonth() === this.today.getMonth()) {
            this.thCell.classList.add("today-bg");
        }
        this.monthsInWeek.push((new Date(this.year, this.month, this.day+(this.n*14)+i)).getMonth());
        this.yearsInWeek.push((new Date(this.year, this.month, this.day+(this.n*14)+i)).getFullYear());
        this.thCellDiv.appendChild(this.thCellTextDate);
        this.thCellDiv2.appendChild(this.thCellTextDay);
        this.thCellDiv.classList.add("bold-font");
        this.thCellDiv2.classList.add("regular-font");
        this.thCell.appendChild(this.thCellDiv);
        this.thCell.appendChild(this.thCellDiv2);
        this.row.appendChild(this.thCell);
      }
      this.hdr.appendChild(this.row);
      this.removeDuplicates(this.monthsInWeek);
      this.removeDuplicatesY(this.yearsInWeek);
      if (this.noDuplicates.length === 2 && this.noDuplicatesY.length === 2) {
       this.displayedDate.innerHTML = this.monthNames[this.noDuplicates[0]] + " " + this.noDuplicatesY[0] + " / " + this.monthNames[this.noDuplicates[1]] + " " + this.noDuplicatesY[1];
      } else if (this.noDuplicates.length === 2 && this.noDuplicatesY.length === 1) {
       this.displayedDate.innerHTML = this.monthNames[this.noDuplicates[0]] + "/" + this.monthNames[this.noDuplicates[1]] + " " + this.noDuplicatesY[0];
      } else { this.displayedDate.innerHTML = this.monthNames[this.noDuplicates[0]] + " " + this.noDuplicatesY[0]; }

      this.tbl.innerHTML = "";
      for (let l = 0; l < 7; l++) {
      this.row = document.createElement("tr");
        for (let p = 0; p < 14; p++) {
          this.tdCell = document.createElement("td");
          this.tdCell.setAttribute("name", (new Date(this.year, this.month, this.day+(this.n*14)+l)).toLocaleDateString("en-US", this.dateNameFormat));
          if ((new Date(this.year, this.month, this.day+(this.n*14)+p)).getDate() === this.today.getDate()
          && (new Date(this.year, this.month, this.day+(this.n*14)+p)).getFullYear() === this.today.getFullYear()
          && (new Date(this.year, this.month, this.day+(this.n*14)+p)).getMonth() === this.today.getMonth()) {
              this.tdCell.classList.add("today-bg");
          }
          this.row.appendChild(this.tdCell);
        }
        this.row.setAttribute("name", "id-" + (l+1));
        this.tbl.appendChild(this.row);
      }
    }
  }
}

</script>

<style scoped>

  th {
    color: #000000;
  }
  td {
    color: #6f6f6f;
  }
  .today-bg {
    background: #E1E7FB;
  }

</style>
