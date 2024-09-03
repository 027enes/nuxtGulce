<template>
  <div>
    <DropdownMenu>
      <DropdownMenuTrigger>Export</DropdownMenuTrigger>
      <DropdownMenuContent>
        <DropdownMenuItem>Tüm Listeyi İndir</DropdownMenuItem>
        <DropdownMenuItem>Katılacakları İndir</DropdownMenuItem>
        <DropdownMenuItem>Katılmayacakları İndir</DropdownMenuItem>
      </DropdownMenuContent>
    </DropdownMenu>
  </div>
</template>

<script setup>
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