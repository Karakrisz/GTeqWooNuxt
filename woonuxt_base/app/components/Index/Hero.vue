<template>
    <section class="relative z-10 w-full h-[800px] overflow-hidden hero px-6 md:px-0">
        <div class="container mx-auto h-full">
            <NuxtImg src="/img/hero.svg" format="svg" class="absolute inset-0 object-cover w-full h-full pointer-events-none"/>
        </div>
    </section>
</template>

<style scoped>
.hero {
   border-radius: 1.5em;
}

.hero .container {
    position: relative;
    border-radius: 1.5em;
    overflow: hidden;
}

/* Mobil nézetben kisebb margin */
@media (max-width: 768px) {
    .hero {
        margin-left: 0;
        margin-right: 0;
    }
}
</style>