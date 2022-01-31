<template>
  <section class="text-gray-600 body-font">
    <div class="container px-5 py-24 mx-auto">
      <div class="flex flex-wrap -m-4">
        <!-- Hotel Card -->
        <p v-if="$fetchState.pending">Chargement....</p>

        <div
          v-else
          v-for="(hotel, index) in filterPublished(data)"
          :key="index"
          class="p-4 md:w-1/3"
        >
          <HotelCard :hotel="hotel" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
const base = require('airtable').base('apppNx4lFeaLhf4Mn');

export default {
  name: 'HotelList',
  //@TODO : Create Loading Component
  //@TODO : Create Json debug component

  data() {
    return {
      data: [],
    }
  },

  async fetch() {
    var _this = this

    base('Places')
      .select({
        view: 'Grid view',
      })
      .eachPage(
        function page(records, next) {
          records.forEach(function (record) {
            try {
              _this.data.push(record)
            } catch (error) {
              console.error(error)
            }
          })

          try {
            next()
          } catch (error) {
            console.error(error)
            return
          }
        },

        function done(err) {
          //@TODO : Handle Error
          if (err) {
            console.error(err)
            return
          }
          //return(data);
        }
      )
    //return data;
  },
  fetchOnServer: false,

  methods: {
    filterPublished(recordsArr) {
      let ret = []
      recordsArr.forEach((e) => {
        if (e.fields.Status == 'Published') {
          ret.push(e)
        }
      })
      return ret
    },
  },
}
</script>
