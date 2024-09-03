<template>
  <div class="navbar navbar-expand-md d-print-none" >
    <div class="container-xl">
      <h1 class="navbar-brand navbar-brand-autodark d-none-navbar-horizontal pe-0 pe-md-3">
        <nuxt-link to="/events">
          <nuxt-icon name="logo/gulce"  class="gulce-logo w-auto h-16" />
        </nuxt-link>
      </h1>

      <DropdownMenu>
        <div class="navbar-nav flex-row order-md-last">
          <DropdownMenuTrigger>
          <div class="nav-item dropdown">
            <div class="nav-link d-flex lh-1 text-reset p-0" data-bs-toggle="dropdown" aria-label="Open user menu">
              <span class="avatar avatar-sm" style="background-image: url(https://ui-avatars.com/api/?background=0D8ABC&color=fff&name=Enes%20İnan)"></span>
              <div class="d-none d-xl-block ps-2">
                <div>Enes İnan</div>
                <div class="mt-1 small text-secondary">Developer</div>
              </div>
            </div>
          </div>
          </DropdownMenuTrigger>
          <DropdownMenuContent>
            <nuxt-link to="/" class="d-flex items-center p-2 text-black justify-center">
                <LogOut class="mr-1 h-3 w-3" />
                <span>Log out</span>
            </nuxt-link>
          </DropdownMenuContent>
        </div>
      </DropdownMenu>

    </div>
  </div>
</template>

<script setup>
import { LogOut } from 'lucide-vue-next';
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuLabel,
  DropdownMenuSeparator,
  DropdownMenuTrigger,
} from '@/components/ui/dropdown-menu'
</script>

<style lang="scss" scoped>

</style>