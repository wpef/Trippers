<template>
  <div
    class="h-full border-2 border-gray-200 border-opacity-60 rounded-lg overflow-hidden"
  >
    <img
      class="lg:h-48 md:h-36 w-full object-cover object-center"
      :src="picture ? picture.url : '#'"
      alt="blog"
    />
    <div class="p-6">
      <h2
        class="tracking-widest text-xs title-font font-medium text-gray-400 mb-1"
      >
        {{ data.Place }}
      </h2>
      <h1 class="title-font text-lg font-medium text-gray-900 mb-3">
        {{ data.Name }}
      </h1>
      <p class="leading-relaxed mb-3 truncate ...">{{ data['Short desc'] }}</p>
      <div class="flex items-center flex-wrap">
        <UtilsLearnMore :link="link" :label="'Voir plus'" />
        <span
          class="text-gray-400 mr-3 inline-flex items-center lg:ml-auto md:ml-0 ml-auto leading-none text-sm pr-3 py-1"
        >
          À partir de {{ data['Starting price'] }} €
        </span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['hotel'],

  data() {
    console.log(this.hotel)
    return {
      data: this.hotel.fields,
      link: '/hotel/' + this.hotel.id,
      picture: this.hotel.fields['Main picture']
        ? this.hotel.fields['Main picture'][0]
        : false,
    }
  },
}
</script>
