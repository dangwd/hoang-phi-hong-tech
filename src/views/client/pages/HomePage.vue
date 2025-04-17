<script setup>
import API from '@/api/api-main';
import { formatPrice } from '@/helper/formatPrice';
import { onMounted, ref } from 'vue';
import ProductsGrid from '../components/ProductsGrid.vue';
import SlidesItem from '../components/SlidesItem.vue';
onMounted(() => {
    fetchAllProducts();
});
const responsiveOptions = ref([
    {
        breakpoint: '1400px',
        numVisible: 2,
        numScroll: 1
    },
    {
        breakpoint: '1199px',
        numVisible: 3,
        numScroll: 1
    },
    {
        breakpoint: '767px',
        numVisible: 2,
        numScroll: 1
    },
    {
        breakpoint: '575px',
        numVisible: 1,
        numScroll: 1
    }
]);
const Products = ref([]);
const SectionData = ref([
    {
        title: ''
    },
    {
        title: 'Danh mục HOT'
    }
]);
const fetchAllProducts = async () => {
    try {
        const res = await API.get(`products?skip=0&limit=2000`);
        Products.value = res.data.metadata.result;
    } catch (error) {
        console.log(error);
    }
};
</script>
<template>
    <body class="font-montserrat container mx-auto text-sm bg-white dark:bg-zinc-900 flex flex-col gap-5">
        <div class="pb-5">
            <SlidesItem></SlidesItem>
        </div>
        <div class="flex flex-col gap-5">
            <section class="w-full">
                <div class="flex justify-between gap-2">
                    <router-link to="/client/products-list">
                        <img width="250" :src="'https://cdn.hoanghamobile.com/i/home/Uploads/2025/04/17/sanphamhot-a06-a16-5g.png'" class="hover:scale-110 transition-all ease-in-out duration-300" />
                    </router-link>
                    <router-link to="/client/new-products">
                        <img width="250" :src="'https://cdn.hoanghamobile.com/i/home/Uploads/2025/04/11/ipad-gen-10.png'" class="hover:scale-110 transition-all ease-in-out duration-300" />
                    </router-link>

                    <router-link to="/client/new-products">
                        <img width="250" :src="'https://cdn.hoanghamobile.com/i/home/Uploads/2025/03/05/sanphamhot2-reno13f-2.png'" class="hover:scale-110 transition-all ease-in-out duration-300" />
                    </router-link>
                    <router-link to="/client/new-products">
                        <img width="250" :src="'https://cdn.hoanghamobile.com/i/home/Uploads/2025/03/25/sanphamhot2.png'" class="hover:scale-110 transition-all ease-in-out duration-300" />
                    </router-link>
                </div>
            </section>

            <div class="flex min-h-auto 2xl:max-w-screen-2xl 2xl:mx-auto 2xl:border-x-2 2xl:border-gray-200 dark:2xl:border-zinc-700">
                <img class="object-cover mr-2 h-96" src="https://cdn.hoanghamobile.com/Uploads/2025/04/15/m4-tc-w.png;trim.threshold=0;trim.percentpadding=0;width=480;" alt="" />
                <div class="">
                    <ProductsGrid :layout="true" :data="Products"></ProductsGrid>
                </div>
            </div>
            <div class="flex min-h-auto 2xl:max-w-screen-2xl 2xl:mx-auto 2xl:border-x-2 2xl:border-gray-200 dark:2xl:border-zinc-700">
                <div class="">
                    <ProductsGrid :layout="true" :data="Products"></ProductsGrid>
                </div>
                <img class="object-cover ml-2 h-96" src="https://cdn.hoanghamobile.com/Uploads/2025/04/09/s25-ultra-461x398-1.png;trim.threshold=0;trim.percentpadding=0;width=480;" alt="" />
            </div>
            <ProductsGrid :data="Products"></ProductsGrid>

            <div>
                <Carousel :value="Products" :numVisible="2" :numScroll="1" :responsiveOptions="responsiveOptions" circular :autoplayInterval="3000">
                    <template #item="slotProps">
                        <div class="border border-surface-200 dark:border-surface-700 rounded m-2 p-4">
                            <div class="mb-4">
                                <div class="relative mx-auto">
                                    <img :src="slotProps.data.images[0]" class="object-contain mx-auto rounded" />
                                </div>
                            </div>
                            <div class="mb-4 font-medium">{{ slotProps.data.productName }}</div>
                            <div class="flex justify-between items-center">
                                <div class="mt-0 font-semibold text-xl">{{ formatPrice(slotProps.data.price) }}</div>
                            </div>
                        </div>
                    </template>
                </Carousel>
            </div>
        </div>
    </body>
</template>
