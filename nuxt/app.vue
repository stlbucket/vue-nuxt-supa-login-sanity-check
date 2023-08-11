<template>
  <div>
    <button @click="onSendMagicLink">Send Magic Link</button>
  </div>
</template>

<script setup lang="ts">
  const supabase = useSupabaseClient()  
  
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
