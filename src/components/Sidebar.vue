<template>
    <aside
        :class="sidebarToggle ? 'translate-x-0' : '-translate-x-full'"
        class="absolute left-0 top-0 z-50 flex h-screen flex-col overflow-y-hidden bg-white duration-300 ease-linear lg:static lg:translate-x-0 w-72 shadow-md text-def">

        <!-- ? Sidebar Header -->
        <div class="flex items-center justify-between gap-2 px-6 py-5 lg:py-6">
            <RouterLink to="/" class="flex gap-2 items-center font-semibold text-xl icon-nav">
                <img src="../assets/app-logo.png" alt="Logo" class="w-12" />
                Absensi Qr Code
            </RouterLink>

            <button class="block lg:hidden" :class="{'lg:block' : sidebarToggle}" @click="$emit('toggleSidebar')">
                <i class="pi pi-arrow-left text-lg"></i>
            </button>
        </div>

        <div class="flex flex-col overflow-y-auto duration-300 ease-linear">

            <!-- Sidebar Menu -->
            <nav class="mt-5 px-4 lg:mt-9 lg:px-6">

                <!-- Menu Group -->
                <div v-for="sidebarItem in sidebarItems" :key="sidebarItem.label">
                    <h3 class="mb-4 ml-4 text-sm font-medium">{{sidebarItem.label}}</h3>

                    <ul class="mb-6 flex flex-col gap-1">
                        <!-- Menu Item -->
                        <li v-for="menuItem in sidebarItem.items" :key="menuItem.label" >
                            <RouterLink class="group relative flex items-center gap-2 rounded-sm px-4 py-2 font-medium duration-300 ease-in-out menu"
                                :to="menuItem.route"
                            >
                                <i class="text-lg" :class="menuItem.icon"></i>

                                {{menuItem.label}}
                            </RouterLink>
                        </li>

                    </ul>
                </div>

            </nav>

        </div>
    </aside>

</template>

<script>
export default {
    props: [
        'sidebarToggle'
    ],
    emits: ['toggleSidebar'],
    data() {
        return {
            sidebarItems: [
                {
                    label: 'Home',
                    items: [
                        {
                            label: 'Dashboard',
                            icon: 'pi pi-home',
                            route: '/'
                        }
                    ]
                },
                {
                    label: 'Absensi',
                    items: [
                        {
                            label: 'QR CODE',
                            icon: 'pi pi-qrcode',
                            route: '/absensi/qr-code'
                        },
                    ]
                },
                {
                    label: 'Pegawai',
                    items: [
                        {
                            label: 'Daftar Pegawai',
                            icon: 'pi pi-users',
                            route: '/pegawai/daftar'
                        },
                        {
                            label: 'Gaji',
                            icon: 'pi pi-wallet',
                            route: '/pegawai/gaji'
                        }
                    ]
                },
                {
                    label: 'Produktifitas',
                    items: [
                        {
                            label: 'Workspaces',
                            icon: 'pi pi-briefcase',
                            route: '/produktifitas/workspaces'
                        },
                        {
                            label: 'Kanban',
                            icon: 'pi pi-list',
                            route: '/produktifitas/kanban'
                        },
                    ]
                },
            ]
        }
    },
    methods: {
        toggleSidebar() {
            this.$emit('toggleSidebar')
        }
    }
}
</script>

<style>
    .icon-nav {
        color: #334155;
        @apply font-medium
    }
</style>