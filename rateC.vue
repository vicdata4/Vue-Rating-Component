<template>
  <div class="btn-group rate">
    <button @click="showButton" type="button" class="btn btn-danger align-ele">
      {{ textVote }}<i class="material-icons">&#xe5c5;</i>
    </button>
    <button @click="showButton" class="btn btn-info" v-if="showNremove"><i class="material-icons">&#xe838;</i>{{rate}}</button>
    <button @click="showButton" v-if="showAdvert" class="btn btn-info">You need to be logged</button>
    <button @click="rating(0)" class="trash" v-if="showNremove"><i class="material-icons">&#xe872;</i></button>
    <div class="btn-toolbar io" role="toolbar" aria-label="rate" v-if="show">
      <div class="btn-group mr-2 overflow" role="group">
        <button v-for="n in 10" @click="rating(n)" type="button" v-bind:class="chooseColor(n)">{{n}}</button>
      </div>
    </div>
  </div>
</template>
<script type="text/javascript">

export default {
  props: ['info'],
  data () {
    return {
      textVote: 'Rate',
      rate: '',
      showNremove: false,
      show: false,
      showAdvert: false,
      logged: true
    }
  },
  methods: {
    showButton () {
      if (!this.show) {
        if (!this.logged) {
          if (!this.showAdvert) {
            this.showAdvert = true
            setTimeout(() => {
              this.showAdvert = false
            }, 3000)
          } else {
            this.showAdvert = false
          }
        } else {
          this.show = true
        }
      } else {
        this.show = false
      }
    },
    rating (score) {
      if (score === 0) {
        var dlete = confirm('Are you sure?')
        if (dlete) {
          this.rate = ''
          this.textVote = 'Rate'
          this.showNremove = false
          this.show = false
        }
      } else {
        this.rate = score
        this.textVote = 'Rated'
        this.showNremove = true
        this.show = false
      }
    },
    chooseColor (n) {
      if (n < 4) {
        return 'btn btn-default'
      } else if (n >= 4 && n < 7) {
        return 'btn btn-warning'
      } else {
        return 'btn btn-success'
      }
    }
  }
}
</script>
<style scoped lang='scss'>
@import "assets/sass/colors.scss";

.align-ele {
  display:flex;
  align-items:center;
}
.overflow {
  overflow-x:auto;
  overflow-y: hidden;
}
.rate {
  display: flex;
  flex-flow: row wrap;
}

.trash {
  margin-left: 15px;
  margin-right: 15px;
  color: $redColor;
  text-decoration: none;
  background: none;
  border: none;
}
.trash:hover {
  color: $redColor;
}

.io {
  margin-top: 10px;
}
@media screen and (min-width: 640px) {
  .io {
    margin-top: 0;
  }
}
</style>
