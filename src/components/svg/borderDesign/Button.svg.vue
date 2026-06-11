<template>
  <div class="relative w-full h-full max-w-50 max-h-15 overflow-hidden group">
    <svg
      viewBox="0 0 331 87"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
      preserveAspectRatio="none"
      class="absolute inset-0 w-full h-full pointer-events-none"
    >
      <path
        d="M2 28.4279V85H301.716L329 48.2488V2H23.9102L2 28.4279Z"
        stroke="#FCC600"
        stroke-width="4"
        vector-effect="non-scaling-stroke"
        class="group-hover:fill-(--primary) transition-colors duration-300"
      />
    </svg>
    <div
      class="relative z-10 w-full h-full overflow-auto text-xl text-center text-(--text-color) hover:text-(--text-dark) hover:font-medium transition-all duration-150"
    >
      <slot />
    </div>
  </div>
</template>
<style></style>
