<template>
    <div class="v-table">
      <div class="v-table__header">
        <p @click="sortByName">Name
          <i class="material-icons">unfold_more</i>
        </p>
        <p @click="sortByPointsEarned">Points earned
          <i class="material-icons">unfold_more</i>
        </p>
        <p @click="sortByPointsSpent">Points spent
          <i class="material-icons">unfold_more</i>
        </p>
        <p @click="sortByDate">Registration date
          <i class="material-icons">unfold_more</i>
        </p>
      </div>
      <div class="v-table__body">
        <v-table-row 
          v-for="row in paginatedUser"
          :key="row.id"
          :row_data="row"
        />
      </div>
      <div class="v-table__pagination">
        <div 
          class="page"
          v-for="page in pages"
          :key="page"
          :class="{'page__selected': page === pageNumber}"
          @click="pageClick(page)"
        >{{page}}</div>
      </div>
    </div>
</template>

<script>
import vTableRow from './v-table-row'

export default {
  data: () => ({
    usersPerPage: 10,
    pageNumber: 1,
    sortName: true,
    sortPointsEarned: true,
    sortPointsSpent: true,
    sortDate: true
  }),
  props: {
    users_data: {
      type: Array,
      default: () => []
    }
  },
  components: {
    vTableRow
  },
  computed: {
    pages() {
      let countPages = Math.ceil(this.users_data.length / 10);
      let newPagesArr = [];
      for( let i = 1; i <= countPages; i++ ) {
        newPagesArr.push(i);
      }
      let from = 2;
      let to = 5;

      if( this.pageNumber - 2 > 0 && this.pageNumber + 1 < countPages ) {
        from = this.pageNumber - 1;
        to = this.pageNumber + 3;
      } else if( this.pageNumber > countPages-3 && this.pageNumber > 1 ) {
        from = this.pageNumber - 1;
        to = countPages - this.pageNumber;

        if( this.pageNumber == countPages ) {
          to = (countPages + 1) - this.pageNumber;
        }
      }

      return [].concat([1], newPagesArr.slice(from - 1, to - 2), [countPages])
    },
    paginatedUser() {
      let from = (this.pageNumber - 1) * this.usersPerPage;
      let to = from + this.usersPerPage;

      return this.users_data.slice(from, to);
    }
  },
  methods: {
    pageClick(page) {
      this.pageNumber = page
    },
    sortByName() {
      if(this.sortName) {
        this.users_data.sort((a,b) => a.name.localeCompare(b.name))
        this.sortName = false
      } else {
        this.users_data.sort((a,b) => b.name.localeCompare(a.name))
        this.sortName = true
      }
    },
    sortByPointsEarned() {
      if(this.sortPointsEarned) {
        this.users_data.sort((a,b) => a.points_earned - b.points_earned)
        this.sortPointsEarned = false
      } else {
        this.users_data.sort((a,b) => b.points_earned - a.points_earned)
        this.sortPointsEarned = true
      }
    },
    sortByPointsSpent() {
      if(this.sortPointsSpent) {
        this.users_data.sort((a,b) => a.points_spent - b.points_spent)
        this.sortPointsSpent = false
      } else {
        this.users_data.sort((a,b) => b.points_spent - a.points_spent)
        this.sortPointsSpent = true
      }
    },
    sortByDate() {
      if(this.sortDate) {
        this.users_data.sort((a,b) => a.registration_date.localeCompare(b.registration_date))
        this.sortDate = false
      } else {
        this.users_data.sort((a,b) => b.registration_date.localeCompare(a.registration_date))
        this.sortDate = true
      }
    }
  }
  
}
</script>

<style lang="scss">
.v-table {
  max-width: 900px;
  margin: 0 auto;
}

.v-table__header {
  display: flex;
  justify-content: space-around;
  border-bottom: 1px solid #e7e7e7;
  p {
    display: flex;
    align-items: center;
    flex-basis: 25%;
    text-align: left;
    cursor: pointer;
  }
}

.v-table__pagination {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 30px;
}

.page {
  padding: 8px;
  margin-right: 10px;
  border: 1px solid #e7e7e7;
  &:hover {
    background: #aeaeae;
    cursor: pointer;
    color: #ffffff;
  }
}
.page__selected {
  background: #aeaeae;
  cursor: pointer;
  color: #ffffff;
}
</style>
