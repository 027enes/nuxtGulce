<template>
  <div>
    <form class="w-full space-y-2" @submit.prevent="onSubmit"> <!-- Prevent default action -->
      <FormField v-slot="{ componentField }" name="email">
        <FormItem v-auto-animate>
          <FormControl>
            <Input type="text" placeholder="Email-Telefon" v-bind="componentField" />
          </FormControl>
          <FormMessage />
        </FormItem>
      </FormField>
      <FormField v-slot="{ componentField }" name="password">
        <FormItem v-auto-animate>
          <FormControl>
            <Input type="password" placeholder="Şifre" v-bind="componentField" />
          </FormControl>
          <FormMessage />
        </FormItem>
      </FormField>
      <div class="flex items-center space-x-2 my-3">
        <Checkbox id="terms" class="w-3 h-3"/>
        <label
            for="terms"
            class="text-sm font-medium leading-none peer-disabled:cursor-not-allowed peer-disabled:opacity-70"
        >
          Accept terms and conditions
        </label>
      </div>
      <Button type="submit">
        Submit
      </Button>
    </form>
  </div>
</template>

<script setup>
import { h } from 'vue'
import { useForm } from 'vee-validate'
import { toTypedSchema } from '@vee-validate/zod'
import * as z from 'zod'
import { useRouter } from 'vue-router'
import { vAutoAnimate } from '@formkit/auto-animate/vue'
import { Checkbox } from '@/components/ui/checkbox'
import { Button } from '@/components/ui/button'
import {
  FormControl,
  FormField,
  FormItem,
  FormMessage,
} from '@/components/ui/form'
import { Input } from '@/components/ui/input'
import { toast } from '@/components/ui/toast'

// Define the schema
const formSchema = toTypedSchema(z.object({
  email: z.string()
      .min(2, 'Email ya da Telefon Numarası Giriniz')
      .max(50),
  password: z.string()
      .min(2, 'Şifre Giriniz')
      .max(50),
}))

const { handleSubmit, validate } = useForm({
  validationSchema: formSchema,
})

// Use the Vue Router for navigation
const router = useRouter()

const onSubmit = handleSubmit((values, { setFieldError }) => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!emailRegex.test(values.email)) {
    setFieldError('email', 'Email adresi geçerli değil')
    return
  }

  // Simulate successful form submission
  toast({
    title: 'You submitted the following values:',
    description: h('pre', { class: 'mt-2 w-[340px] rounded-md bg-slate-950 p-4' }, h('code', { class: 'text-white' }, JSON.stringify(values, null, 2))),
  })

  // Redirect to a different page after successful submission
  router.push('/events/')
})
</script>

<style lang="scss" scoped>

</style>
