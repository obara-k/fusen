<template>
  <div class="column">
    <div class="card">
      <header class="card-header">
        <p class="card-header-title has-text-grey">
          {{ name }}
        </p>
        <div class="content has-text-centered">

        </div>
      </header>
      <div class="card-content">
        <div class="card-content-inner">
          <div>{{ icon }}</div>
            <ul>
              <li>{{ latestDate }}</li>
              <li>{{ latestTenki }}</li>
          </ul>
        </div>
        <slot />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true
    },
    icon: {
      type: String,
      required: true
    },
    latestDate: {
      type: String,
      required: true
    },
    latestTenki: {
      type: String,
      required: true
    }
  }
}
</script>
