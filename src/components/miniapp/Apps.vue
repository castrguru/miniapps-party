<template>
    <main class="w-full h-full px-2 pb-7 flex flex-col gap-6 overflow-y-scroll overflow-x-hidden">
        <div v-if="App && App.length > 0">
            <ClientOnly>
                <button v-if="spotlight" @click="viewDetail(spotlight.hostname)" class="cursor-pointer w-full mt-2 px-3 py-3 flex gap-3 bg-gradient-to-r from-lime-100 to-lime-50 border-2 border-lime-300 rounded-md hover:from-amber-100 hover:to-amber-50">
                    <img :src="spotlight.iconUrl" class="size-32 border-2 border-lime-300 rounded-md" />

                    <div class="w-full flex flex-col items-center flex-1">
                        <h2 class="text-sky-800 font-bold text-3xl tracking-wider">
                            {{spotlight.appName}}
                        </h2>

                        <h3 class="text-sky-400 font-bold text-lg tracking-wider">
                            {{spotlight.tagline || spotlight.hostname}}
                        </h3>

                        <!-- <h3 class="text-sky-600 font-bold text-base tracking-wider italic">
                            added {{moment.unix(spotlight.createdAt).fromNow()}}
                        </h3> -->
                    </div>
                </button>
            </ClientOnly>

            <h3 class="text-center my-5 text-rose-200 font-bold text-lg tracking-wider">
                <span class="text-rose-300 font-extrabold text-xl">TOP3 <a href="/bangers">Bangers!</a></span> Since Yesterday<span class="text-3xl">↴</span>
            </h3>

<!-- BEGIN FEATURED -->
            <ClientOnly>
                <button v-for="app of featured" :key="app.hostname" @click=viewDetail(app.hostname) class="relative cursor-pointer w-full mt-5 px-2 py-2 flex items-center gap-3 bg-gradient-to-r from-sky-100 to-sky-50 border-2 border-slate-700 rounded-md hover:from-amber-100 hover:to-amber-50">
                    <img :src="app.iconUrl" class="size-16 bg-slate-900 border border-slate-700 rounded-md" />

                    <div class="pr-[120px] w-full flex flex-col items-start flex-1">
                        <h2 class="text-sky-800 font-bold text-2xl tracking-tighter text-left line-clamp-1">
                            {{app.appName}}
                        </h2>

                        <h3 class="text-sky-400 font-bold text-sm tracking-wider text-left line-clamp-1">
                            {{app.tagline || app.hostname}}
                        </h3>

                        <h3 class="text-sky-600 font-bold text-xs tracking-tighter italic">
                            added {{moment.unix(app.createdAt).fromNow()}}
                        </h3>
                    </div>

                    <img v-if="app.heroImageUrl" :src="app.heroImageUrl" class="absolute right-2 h-16 border border-slate-700 rounded-md" />
                </button>
            </ClientOnly>
<!-- END FEATURED -->

            <h3 class="text-center my-5 text-rose-200 font-bold text-lg tracking-wider">
                New &amp; Noteworthy <span class="text-rose-300 font-extrabold text-xl">LIVE! Feed<span class="text-3xl">↴</span></span>
            </h3>

<!-- BEGIN ABOVE THE FOLD -->
            <ClientOnly>
                <button v-for="app of aboveTheFold" :key="app.hostname" @click=viewDetail(app.hostname) class="relative cursor-pointer w-full mt-5 px-2 py-2 flex items-center gap-3 bg-gradient-to-r from-sky-100 to-sky-50 border-2 border-slate-700 rounded-md hover:from-amber-100 hover:to-amber-50">
                    <img :src="app.iconUrl" class="size-16 bg-slate-900 border border-slate-700 rounded-md" />

                    <div class="pr-[120px] w-full flex flex-col items-start flex-1">
                        <h2 class="text-sky-800 font-bold text-2xl tracking-tighter text-left line-clamp-1">
                            {{app.appName}}
                        </h2>

                        <h3 class="text-sky-400 font-bold text-sm tracking-wider text-left line-clamp-1">
                            {{app.tagline || app.hostname}}
                        </h3>

                        <h3 class="text-sky-600 font-bold text-xs tracking-tighter italic">
                            added {{moment.unix(app.createdAt).fromNow()}}
                        </h3>
                    </div>

                    <img v-if="app.heroImageUrl" :src="app.heroImageUrl" class="absolute right-2 flex-0 h-16 border border-slate-700 rounded-md" />
                </button>
            </ClientOnly>
<!-- END ABOVE THE FOLD -->

            <ClientOnly>
                <button v-if="sponsored" @click="viewDetail(sponsored.hostname)" class="cursor-pointer w-full my-8 px-3 py-3 flex gap-3 bg-gradient-to-r from-stone-200 to-stone-50 border-4 border-stone-300 rounded-md hover:from-stone-800 hover:to-stone-600">
                    <img :src="sponsored.iconUrl" class="size-32 border-2 border-stone-500 rounded-md" />

                    <div class="w-full flex flex-col items-center flex-1">
                        <h2 class="text-sky-800 font-bold text-3xl tracking-wider">
                            {{sponsored.appName}}
                        </h2>

                        <h3 class="text-sky-400 font-bold text-sm tracking-wider">
                            {{sponsored.tagline || sponsored.hostname}}
                        </h3>

                        <!-- <h3 class="text-sky-600 font-bold text-base tracking-tighter italic">
                            added {{moment.unix(sponsored.createdAt).fromNow()}}
                        </h3> -->
                    </div>

                    <img v-if="sponsored.heroImageUrl" :src="sponsored.heroImageUrl" class="h-16 border border-slate-700 rounded-md" />
                </button>
            </ClientOnly>

<!-- BEGIN BELOW THE FOLD -->
            <ClientOnly>
                <button v-for="app of belowTheFold" :key="app.hostname" @click=viewDetail(app.hostname) class="relative cursor-pointer w-full mt-5 px-2 py-2 flex items-center gap-3 bg-gradient-to-r from-sky-100 to-sky-50 border-2 border-slate-700 rounded-md hover:from-amber-100 hover:to-amber-50">
                    <img :src="app.iconUrl" class="size-16 bg-slate-900 border border-slate-700 rounded-md" />

                    <div class="pr-[120px] w-full flex flex-col items-start flex-1">
                        <h2 class="text-sky-800 font-bold text-2xl tracking-tighter text-left line-clamp-1">
                            {{app.appName}}
                        </h2>

                        <h3 class="text-sky-400 font-bold text-sm tracking-wider text-left line-clamp-1">
                            {{app.tagline || app.hostname}}
                        </h3>

                        <h3 class="text-sky-600 font-bold text-xs tracking-tighter italic">
                            added {{moment.unix(app.createdAt).fromNow()}}
                        </h3>
                    </div>

                    <img v-if="app.heroImageUrl" :src="app.heroImageUrl" class="absolute right-2 h-16 border border-slate-700 rounded-md" />
                </button>
            </ClientOnly>
<!-- END BELOW THE FOLD -->

            <section class="my-5 w-full px-10 grid grid-cols-2 gap-0.5">
                <a href="#" class="opacity-30 cursor-not-allowed group px-5 py-2 flex justify-center items-center bg-amber-100 rounded-lg rounded-r-none">
                    <span span class="flex flex-row items-center gap-2 text-amber-500 font-bold text-2xl uppercase">
                        <svg class="size-6" data-slot="icon" fill="none" stroke-width="1.5" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                            <path stroke-linecap="round" stroke-linejoin="round" d="m11.25 9-3 3m0 0 3 3m-3-3h7.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"></path>
                        </svg>

                        Newer
                    </span>
                </a>

                <a href="/apps/page2" class="group px-5 py-2 flex flex-row justify-center items-center bg-amber-100 rounded-lg rounded-l-none hover:bg-amber-600">
                    <span span class="flex flex-row items-center gap-2 text-amber-500 font-bold text-2xl uppercase group-hover:text-amber-50">
                        Older

                        <svg class="size-6" data-slot="icon" fill="none" stroke-width="1.5" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                            <path stroke-linecap="round" stroke-linejoin="round" d="m12.75 15 3-3m0 0-3-3m3 3h-7.5M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"></path>
                        </svg>
                    </span>
                </a>
            </section>
        </div>
        <div v-else>
            <h2 class="text-slate-200 font-bold text-2xl tracking-widest">
                now loading mini apps...
            </h2>
        </div>

    </main>
</template>

<script setup lang="ts">
/* Import modules. */
import { computed, onMounted, ref } from 'vue'
import { useStore } from '@nanostores/vue'
import { sdk } from '@farcaster/frame-sdk'
import moment from 'moment'

import $App from '../../stores/app'

/* Request Mini App flag. */
// TODO Maybe we set a SESSION flag??
const isMiniApp = await sdk.isInMiniApp()

/* Define properties. */
// https://vuejs.org/guide/components/props.html#props-declaration
const props = defineProps({
    cursor: String,
})

const App = useStore($App)

// const HERO_HOSTNAME_MAX_LEN = 20
// const NOHERO_HOSTNAME_MAX_LEN = 30

const spotlight = ref()
const sponsored = ref()

const featured = computed(() => $App.get().slice(0, 3))
const aboveTheFold = computed(() => $App.get().slice(3, 16))
const belowTheFold = computed(() => $App.get().slice(16, 18))

const init = async () => {
    console.log('APPS', $App.get())

    spotlight.value = {
        appName: 'Paragraph',
        hostname: 'paragraph.com',
        homeUrl: 'https://paragraph.com/home?frame=true',
        iconUrl: 'https://paragraph.com/branding/v2/logomark.png',
        createdAt: 1749417098,
    }

    sponsored.value = {
        appName: 'frames in blue',
        hostname: 'frames-in-blue.vercel.app',
        homeUrl: 'https://frames-in-blue.vercel.app',
        iconUrl: 'https://frames-in-blue.vercel.app/icon.png',
        createdAt: 1749419076,
    }
}

const viewDetail = async (_hostname) => {
    document.location = '/app/' + encodeURIComponent(_hostname)
}

onMounted(() => {
    init()
})

// onBeforeUnmount(() => {
//     console.log('Before Unmount!')
//     // Now is the time to perform all cleanup operations.
// })
</script>
