<script setup lang="ts">
  import { createClient } from '@supabase/supabase-js'

  const options = {
    db: {
      schema: 'public',
    },
    auth: {
      autoRefreshToken: true,
      persistSession: true,
      detectSessionInUrl: true
    },
    global: {
      headers: { 'x-my-custom-header': 'my-app-name' },
    },
  }
  const supabase = createClient(
    "http://localhost:54321", 
    "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZS1kZW1vIiwicm9sZSI6ImFub24iLCJleHAiOjE5ODM4MTI5OTZ9.CRXP1A7WOeoJeXxjNni43kdQwgnWNReilDMblYTn_I0", 
    options
  )
  
  const onSendMagicLink = async() => {
    const { error } = await supabase.auth.signInWithOtp({
      email: 'test@example.com',
      options: {
        emailRedirectTo: 'http://localhost:3000'
      }
    })
    if (error) {
      alert(error.message)
    } else {
      alert('check your inbox for the magic link')
    }

  }
</script>

<template>
  <button @click="onSendMagicLink">Send Magic Link</button>
</template>

<style scoped>
</style>
