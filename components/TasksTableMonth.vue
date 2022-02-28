<template>

  <div class="wrapper">

    <div class="table-time-nav">
      <h3 class="width">{{ months[currentMonth] }}, {{ currentYear }}</h3>
      <div>
          <button @click="prevMonth()">&#60;</button>
          <button @click="nextMonth()">&#62;</button>
      </div>
    </div>

      <table class="month-table">
          <thead id="calendar-head">
            <tr>
              <th v-for="day in shortWeekDayNames"
                  :key="day.id"
                  >
                  {{ day }}
              </th>
            </tr>
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
      today: new Date(),
      months: ["Январь", "Февраль", "Март", "Апрель", "Май", "Июнь", "Июль", "Август", "Сентябрь", "Октябрь", "Ноябрь", "Декабрь"],
      weekDayNames: ['воскресенье', 'понедельник', 'вторник', 'среда', 'четверг', 'пятница', 'суббота'],
      shortWeekDayNames: ['вс', 'пн', 'вт', 'ср', 'чт', 'пт', 'сб'],
      currentMonth: null, currentYear: null, currentMonthDay: null, currentMonthName: null,
      currentWeekDay: null, firstDay: null, lastDay: null, date: 1,
      row: null, cell: null, cellText: null,
      hdr: null, hdrFirstChild: null, hdrLastChild: null,
      tbl: null, tblChildren: null, tblFirstRow: null, tblLastRow: null,
    }
  },
  mounted: function() {
        setTimeout(() => {
          this.initVar();
        }, 0);
  },
  methods: {
      initVar() {
        this.hdr = document.getElementById("calendar-head");
        this.tbl = document.getElementById("calendar-body");
        this.currentMonth = this.today.getMonth();
        this.currentYear = this.today.getFullYear();
        this.firstDay = (new Date(this.today.getFullYear(), this.today.getMonth(), 1)).getDay();
        this.lastDay = (new Date(this.today.getFullYear(), this.today.getMonth()+1, 0)).getDay();
        this.showCalendar(this.currentMonth, this.currentYear);
      },
      nextMonth() {
          this.currentYear = (this.currentMonth === 11) ? this.currentYear + 1 : this.currentYear;
          this.currentMonth = (this.currentMonth + 1) % 12;
          this.showCalendar(this.currentMonth, this.currentYear);
      },
      prevMonth() {
          this.currentYear = (this.currentMonth === 0) ? this.currentYear - 1 : this.currentYear;
          this.currentMonth = (this.currentMonth === 0) ? 11 : this.currentMonth - 1;
          this.showCalendar(this.currentMonth, this.currentYear);
      },
      daysInMonth(iMonth, iYear)
      {
          return 32 - new Date(iYear, iMonth, 32).getDate();
      },
      showCalendar(month, year) {
      this.firstDay = (new Date(year, month)).getDay();
      this.lastDay = (new Date(year,month+1,0)).getDay();
      this.tbl.innerHTML = ""; // clearing all previous cells

      this.date = 1;
      for (let i = 0; i < 6; i++) {

          this.row = document.createElement("tr");

          for (let j = 0; j < 7; j++) {
            if (i === 0 && j < this.firstDay) {
                this.cell = document.createElement("td");
                this.cellText = document.createTextNode("");
                this.cell.classList.add("bg-grey");
                this.cell.appendChild(this.cellText);
                this.row.appendChild(this.cell);
            }
            else if (this.date > this.daysInMonth(month, year)) {
              if (i < 5) {
                if (this.firstDay === 0 && this.daysInMonth(month, year) === 28) {
                  for (let q = 0; q < 7; q++) {
                    this.cell = document.createElement("td");
                    this.cellText = document.createTextNode("");
                    this.cell.classList.add("bg-grey");
                    this.cell.appendChild(this.cellText);
                    this.row.appendChild(this.cell);
                  }
                  break;
                } else {
                  for (let k = this.lastDay; k < 6; k++) {
                    this.cell = document.createElement("td");
                    this.cellText = document.createTextNode("");
                    this.cell.classList.add("bg-grey");
                    this.cell.appendChild(this.cellText);
                    this.row.appendChild(this.cell);
                  }
                  break;
                }
              }
              if (i === 5 && this.firstDay === 5 && this.daysInMonth(month, year) === 31 || i === 5 && this.firstDay === 6 && this.daysInMonth(month, year) > 29)
              {
                for (let m = this.lastDay; m < 6; m++) {
                  this.cell = document.createElement("td");
                  this.cellText = document.createTextNode("");
                  this.cell.classList.add("bg-grey");
                  this.cell.appendChild(this.cellText);
                  this.row.appendChild(this.cell);
                }
                break;
              }
              else {
                for (let h = 0; h < 7; h++) {
                  this.cell = document.createElement("td");
                  this.cellText = document.createTextNode("");
                  this.cell.classList.add("bg-grey");
                  this.cell.appendChild(this.cellText);
                  this.row.appendChild(this.cell);
                }
                break;
              }
            }
            else {
                this.cell = document.createElement("td");
                this.cellSpan = document.createElement("span");
                this.cellSpan2 = document.createElement("span");
                this.cellText = document.createTextNode(this.date + ')');
                this.cellText2 = document.createTextNode('Lorem ipsum dolor sit amet, consectetur adipisicing elit. Mollitia vitae non dignissimos accusantium exercitationem minus dolores delectus odit nobis asperiores, eligendi enim rem magnam pariatur! Libero eveniet nobis tempore sit.');
                if (this.date === this.today.getDate() && year === this.today.getFullYear() && month === this.today.getMonth()) {
                    this.cell.classList.add("today-bg");
                } // color today's date
                this.cellSpan2.classList.add("regular-font");
                this.cellSpan.appendChild(this.cellText);
                this.cellSpan2.appendChild(this.cellText2);
                this.cell.appendChild(this.cellSpan);
                this.cell.appendChild(this.cellSpan2);
                this.row.appendChild(this.cell);
                this.date++;
            }
          }
          this.tbl.appendChild(this.row);
        }
      this.hdrFirstChild = this.hdr.childNodes[0].children[0];
      this.hdrLastChild = this.hdr.childNodes[0].children[6];
      this.hdrFirstChild.classList.add("unshown");
      this.hdrLastChild.classList.add("unshown");

      for (let rowsCount = 0; rowsCount < 6; rowsCount++) {
        this.tbl.childNodes[rowsCount].children[0].classList.add("unshown");
        this.tbl.childNodes[rowsCount].children[1].classList.add("organize-day-td");
        this.tbl.childNodes[rowsCount].children[2].classList.add("organize-day-td");
        this.tbl.childNodes[rowsCount].children[3].classList.add("organize-day-td");
        this.tbl.childNodes[rowsCount].children[4].classList.add("organize-day-td");
        this.tbl.childNodes[rowsCount].children[5].classList.add("organize-day-td");
        this.tbl.childNodes[rowsCount].children[6].classList.add("unshown");
      }

      this.tblFirstRow = this.tbl.childNodes[0];
      this.tblLastRow = this.tbl.childNodes[5];
      if (this.tblFirstRow.children[1].innerHTML === ""
      && this.tblFirstRow.children[2].innerHTML === ""
      && this.tblFirstRow.children[3].innerHTML === ""
      && this.tblFirstRow.children[4].innerHTML === ""
      && this.tblFirstRow.children[5].innerHTML === ""
      ) { this.tblFirstRow.classList.add("unshown"); }
      else if (this.tblLastRow.children[1].innerHTML === ""
      && this.tblLastRow.children[2].innerHTML === ""
      && this.tblLastRow.children[3].innerHTML === ""
      && this.tblLastRow.children[4].innerHTML === ""
      && this.tblLastRow.children[5].innerHTML === ""
      ) { this.tblLastRow.classList.add("unshown"); }
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

</style>
