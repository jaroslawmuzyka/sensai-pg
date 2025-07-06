# Supabase Cheat Sheet

<details>
<summary>Setup & Installation</summary>

```shell
# JS/TS Client
npm install @supabase/supabase-js

# Auth UI (opcjonalne)
npm install @supabase/auth-ui-react @supabase/auth-ui-shared

# SSR helpers (dla framework SSR)
npm install @supabase/ssr

# CLI (global)
npm install -g @supabase/cli
```

</details>

<details>
<summary>Environment Variables</summary>

```text
# .env.local
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key

# Dla Vite
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key

# SvelteKit
PUBLIC_SUPABASE_URL=https://your-project.supabase.co
PUBLIC_SUPABASE_ANON_KEY=your-anon-key
```

</details>

<details>
<summary>Podstawowy Client Setup</summary>

```javascript
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(
  'https://your-project.supabase.co',
  'your-anon-key'
)

export default supabase
```

</details>

---

## Authentication

<details>
<summary>Podstawowe Auth Operations</summary>

```javascript
// Sign Up
const { data, error } = await supabase.auth.signUp({
  email: 'example@email.com',
  password: 'example-password',
})

// Sign In
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'example@email.com',
  password: 'example-password',
})

// Sign Out
const { error } = await supabase.auth.signOut()

// Get Current User
const { data: { user } } = await supabase.auth.getUser()

// Get Session
const { data: { session } } = await supabase.auth.getSession()
```

</details>

<details>
<summary>OAuth Providers</summary>

```javascript
// Sign in z Google
const { data, error } = await supabase.auth.signInWithOAuth({
  provider: 'google',
  options: {
    redirectTo: 'http://localhost:3000/auth/callback'
  }
})

// Sign in z GitHub
const { data, error } = await supabase.auth.signInWithOAuth({
  provider: 'github'
})
```

</details>

<details>
<summary>Auth State Listening</summary>

```javascript
// Listen for auth changes
supabase.auth.onAuthStateChange((event, session) => {
  if (event === 'SIGNED_IN') {
    console.log('User signed in:', session.user)
  }
  if (event === 'SIGNED_OUT') {
    console.log('User signed out')
  }
})
```

</details>

---

## Database Operations

<details>
<summary>Basic CRUD</summary>

```javascript
// INSERT
const { data, error } = await supabase
  .from('profiles')
  .insert([
    { username: 'john_doe', website: 'https://johndoe.com' }
  ])

// SELECT
const { data, error } = await supabase
  .from('profiles')
  .select('*')

// SELECT with filtering
const { data, error } = await supabase
  .from('profiles')
  .select('username, website')
  .eq('username', 'john_doe')
  .single()

// UPDATE
const { data, error } = await supabase
  .from('profiles')
  .update({ website: 'https://new-website.com' })
  .eq('id', userId)

// DELETE
const { data, error } = await supabase
  .from('profiles')
  .delete()
  .eq('id', userId)
```

</details>

<details>
<summary>Advanced Queries</summary>

```javascript
// Filtering
const { data, error } = await supabase
  .from('posts')
  .select('*')
  .eq('status', 'published')
  .gte('created_at', '2024-01-01')
  .order('created_at', { ascending: false })
  .limit(10)

// Joins
const { data, error } = await supabase
  .from('posts')
  .select(`
    *,
    profiles (
      username,
      avatar_url
    )
  `)

// Full text search
const { data, error } = await supabase
  .from('posts')
  .select('*')
  .textSearch('title', 'supabase')
```

</details>

<details>
<summary>RPC Calls</summary>

```javascript
// Call stored procedure
const { data, error } = await supabase
  .rpc('match_documents', {
    query_embedding: embedding,
    match_threshold: 0.78,
    match_count: 10
  })
```

</details>

---

## Row Level Security (RLS)

<details>
<summary>Enabling RLS</summary>

```sql
-- Enable RLS na tabeli
ALTER TABLE profiles ENABLE ROW LEVEL SECURITY;
```

</details>

<details>
<summary>Basic RLS Policies</summary>

```sql
-- Policy dla SELECT - wszyscy mogą czytać profile
CREATE POLICY "Public profiles are viewable by everyone"
ON profiles FOR SELECT
USING (true);

-- Policy dla INSERT - użytkownicy mogą wstawiać tylko swoje profile
CREATE POLICY "Users can insert their own profile"
ON profiles FOR INSERT
WITH CHECK ((SELECT auth.uid()) = id);

-- Policy dla UPDATE - użytkownicy mogą aktualizować tylko swoje profile
CREATE POLICY "Users can update own profile"
ON profiles FOR UPDATE
USING ((SELECT auth.uid()) = id);

-- Policy dla DELETE - użytkownicy mogą usuwać tylko swoje profile
CREATE POLICY "Users can delete own profile"
ON profiles FOR DELETE
USING ((SELECT auth.uid()) = id);
```

</details>

<details>
<summary>Advanced RLS Policies</summary>

```sql
-- Policy z JWT claims
CREATE POLICY "User is in team"
ON my_table
TO authenticated
USING (team_id IN (SELECT auth.jwt() -> 'app_metadata' -> 'teams'));

-- Policy z joinami (unikaj - wolne)
CREATE POLICY "rls_test_select" ON test_table
TO authenticated
USING (
  team_id IN (
    SELECT team_id
    FROM team_user
    WHERE user_id = (SELECT auth.uid())
  )
);

-- Optimized policy z security definer functions
CREATE OR REPLACE FUNCTION private.get_user_org_role(org_id bigint, user_id uuid)
RETURNS text
SET search_path = ''
AS $$
  SELECT role FROM public.org_members
  WHERE org_id = $1 AND user_id = $2;
$$ LANGUAGE sql SECURITY DEFINER;

CREATE POLICY "Org management restricted to owners"
ON public.organizations FOR ALL USING (
  private.get_user_org_role(id, (SELECT auth.uid())) = 'owner'
);
```

</details>

---

## Realtime

<details>
<summary>Basic Subscriptions</summary>

```javascript
// Subscribe to table changes
const subscription = supabase
  .channel('profiles')
  .on('postgres_changes',
    {
      event: '*',
      schema: 'public',
      table: 'profiles'
    },
    (payload) => {
      console.log('Change received!', payload)
    }
  )
  .subscribe()

// Subscribe to specific changes
const subscription = supabase
  .channel('todos')
  .on('postgres_changes',
    {
      event: 'INSERT',
      schema: 'public',
      table: 'todos',
      filter: 'user_id=eq.' + userId
    },
    (payload) => {
      console.log('New todo:', payload.new)
    }
  )
  .subscribe()

// Unsubscribe
subscription.unsubscribe()
```

</details>

<details>
<summary>Broadcast Messages</summary>

```javascript
// Send broadcast message
const channel = supabase.channel('room1')

channel
  .on('broadcast', { event: 'test' }, (payload) => {
    console.log(payload)
  })
  .subscribe()

// Send message
await channel.send({
  type: 'broadcast',
  event: 'test',
  payload: { message: 'hello world' }
})
```

</details>

<details>
<summary>Presence</summary>

```javascript
// Track user presence
const channel = supabase.channel('room1')

channel
  .on('presence', { event: 'sync' }, () => {
    const newState = channel.presenceState()
    console.log('sync', newState)
  })
  .on('presence', { event: 'join' }, ({ key, newPresences }) => {
    console.log('join', key, newPresences)
  })
  .on('presence', { event: 'leave' }, ({ key, leftPresences }) => {
    console.log('leave', key, leftPresences)
  })
  .subscribe(async (status) => {
    if (status !== 'SUBSCRIBED') { return }

    await channel.track({
      user: 'user-1',
      online_at: new Date().toISOString(),
    })
  })
```

</details>

---

## Storage

<details>
<summary>File Uploads</summary>

```javascript
// Upload file
const { data, error } = await supabase.storage
  .from('avatars')
  .upload('public/avatar1.png', file, {
    cacheControl: '3600',
    upsert: false
  })

// Upload z options
const { data, error } = await supabase.storage
  .from('avatars')
  .upload(`${userId}/avatar.png`, file, {
    contentType: 'image/png',
    cacheControl: '3600',
    upsert: true
  })
```

</details>

<details>
<summary>File Downloads & URLs</summary>

```javascript
// Download file
const { data, error } = await supabase.storage
  .from('avatars')
  .download('public/avatar1.png')

// Get public URL
const { data } = supabase.storage
  .from('avatars')
  .getPublicUrl('public/avatar1.png')

// Get signed URL (dla private files)
const { data, error } = await supabase.storage
  .from('private-bucket')
  .createSignedUrl('path/to/file.pdf', 60) // 60 seconds
```

</details>

<details>
<summary>Storage Policies</summary>

```sql
-- Public access policy
CREATE POLICY "Avatar images are publicly accessible"
ON storage.objects FOR SELECT
USING (bucket_id = 'avatars');

-- Upload policy
CREATE POLICY "Anyone can upload an avatar"
ON storage.objects FOR INSERT
WITH CHECK (bucket_id = 'avatars');

-- User-specific policies
CREATE POLICY "Users can upload their own avatars"
ON storage.objects FOR INSERT
WITH CHECK (
  bucket_id = 'avatars'
  AND (storage.foldername(name))[1] = (SELECT auth.uid()::text)
);
```

</details>

---

## Next.js Integration

<details>
<summary>App Router Setup</summary>

```typescript
// utils/supabase/client.ts
import { createBrowserClient } from '@supabase/ssr'

export function createClient() {
  return createBrowserClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
  )
}
```

```typescript
// utils/supabase/server.ts
import { createServerClient } from '@supabase/ssr'
import { cookies } from 'next/headers'

export async function createClient() {
  const cookieStore = await cookies()

  return createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
    {
      cookies: {
        getAll() {
          return cookieStore.getAll()
        },
        setAll(cookiesToSet) {
          try {
            cookiesToSet.forEach(({ name, value, options }) =>
              cookieStore.set(name, value, options)
            )
          } catch {
            // The `setAll` method was called from a Server Component.
            // This can be ignored if you have middleware refreshing
            // user sessions.
          }
        },
      },
    }
  )
}
```

</details>

<details>
<summary>Middleware (App Router)</summary>

```typescript
// middleware.ts
import { createServerClient } from '@supabase/ssr'
import { NextResponse, type NextRequest } from 'next/server'

export async function middleware(request: NextRequest) {
  let supabaseResponse = NextResponse.next({
    request,
  })

  const supabase = createServerClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!,
    {
      cookies: {
        getAll() {
          return request.cookies.getAll()
        },
        setAll(cookiesToSet) {
          cookiesToSet.forEach(({ name, value, options }) => {
            request.cookies.set(name, value)
            supabaseResponse.cookies.set(name, value, options)
          })
        },
      },
    }
  )

  // IMPORTANT: Avoid writing any logic between createServerClient and
  // supabase.auth.getUser(). A simple mistake could make it very hard to debug
  // issues with users being randomly logged out.

  const {
    data: { user },
  } = await supabase.auth.getUser()

  if (
    !user &&
    !request.nextUrl.pathname.startsWith('/login') &&
    !request.nextUrl.pathname.startsWith('/auth')
  ) {
    // no user, potentially respond by redirecting the user to the login page
    const url = request.nextUrl.clone()
    url.pathname = '/login'
    return NextResponse.redirect(url)
  }

  // IMPORTANT: You *must* return the supabaseResponse object as it is. If you're
  // creating a new response object with NextResponse.next() make sure to:
  // 1. Pass the request in it, like so:
  //    const myNewResponse = NextResponse.next({ request })
  // 2. Copy over the cookies, like so:
  //    myNewResponse.cookies.setAll(supabaseResponse.cookies.getAll())
  // 3. Change the myNewResponse object instead of the supabaseResponse object

  return supabaseResponse
}

export const config = {
  matcher: [
    /*
     * Match all request paths except for the ones starting with:
     * - _next/static (static files)
     * - _next/image (image optimization files)
     * - favicon.ico (favicon file)
     * Feel free to modify this pattern to include more paths.
     */
    '/((?!_next/static|_next/image|favicon.ico|.*\.(?:svg|png|jpg|jpeg|gif|webp)$).*)',
  ],
}
```

</details>

<details>
<summary>Server Actions</summary>

```typescript
// app/auth/actions.ts
'use server'

import { revalidatePath } from 'next/cache'
import { redirect } from 'next/navigation'
import { createClient } from '@/utils/supabase/server'

export async function login(formData: FormData) {
  const supabase = await createClient()

  const data = {
    email: formData.get('email') as string,
    password: formData.get('password') as string,
  }

  const { error } = await supabase.auth.signInWithPassword(data)

  if (error) {
    redirect('/error')
  }

  revalidatePath('/', 'layout')
  redirect('/account')
}

export async function signup(formData: FormData) {
  const supabase = await createClient()

  const data = {
    email: formData.get('email') as string,
    password: formData.get('password') as string,
  }

  const { error } = await supabase.auth.signUp(data)

  if (error) {
    redirect('/error')
  }

  revalidatePath('/', 'layout')
  redirect('/account')
}
```

</details>

---

## Edge Functions

<details>
<summary>Basic Edge Function</summary>

```typescript
// supabase/functions/hello-world/index.ts
import { serve } from 'https://deno.land/std@0.170.0/http/server.ts'

serve(async (req) => {
  const { name } = await req.json()
  const data = {
    message: `Hello ${name}!`,
  }

  return new Response(
    JSON.stringify(data),
    { headers: { "Content-Type": "application/json" } },
  )
})
```

</details>

<details>
<summary>Edge Function z Supabase Client</summary>

```typescript
import { createClient } from 'jsr:@supabase/supabase-js@2'

serve(async (req) => {
  const supabase = createClient(
    Deno.env.get('SUPABASE_URL') ?? '',
    Deno.env.get('SUPABASE_SERVICE_ROLE_KEY') ?? ''
  )

  const { data, error } = await supabase
    .from('countries')
    .select('*')

  if (error) {
    return new Response(JSON.stringify(error), { status: 500 })
  }

  return new Response(JSON.stringify(data), {
    headers: { 'Content-Type': 'application/json' },
  })
})
```

</details>

<details>
<summary>OpenAI Integration</summary>

```typescript
import OpenAI from 'https://deno.land/x/openai@v4.24.0/mod.ts'

serve(async (req) => {
  const { query } = await req.json()

  const openai = new OpenAI({
    apiKey: Deno.env.get('OPENAI_API_KEY'),
  })

  const chatCompletion = await openai.chat.completions.create({
    messages: [{ role: 'user', content: query }],
    model: 'gpt-3.5-turbo',
    stream: false,
  })

  const reply = chatCompletion.choices[0].message.content

  return new Response(reply, {
    headers: { 'Content-Type': 'text/plain' },
  })
})
```

</details>

---

## AI & Vector Search

<details>
<summary>Vector Column Setup</summary>

```sql
-- Create table with vector column
CREATE TABLE documents (
  id BIGSERIAL PRIMARY KEY,
  content TEXT,
  embedding VECTOR(1536) -- OpenAI ada-002 size
);

-- Create vector index
CREATE INDEX ON documents USING hnsw (embedding vector_cosine_ops);
```

</details>

<details>
<summary>Similarity Search Function</summary>

```sql
CREATE OR REPLACE FUNCTION match_documents(
  query_embedding VECTOR(1536),
  match_threshold FLOAT,
  match_count INT
)
RETURNS SETOF documents
LANGUAGE sql STABLE
AS $$
  SELECT *
  FROM documents
  WHERE documents.embedding <=> query_embedding < 1 - match_threshold
  ORDER BY documents.embedding <=> query_embedding
  LIMIT match_count;
$$;
```

</details>

<details>
<summary>Edge Function for Embeddings</summary>

```typescript
const model = new Supabase.ai.Session('gte-small')

serve(async (req) => {
  const { input } = await req.json()

  // Generate embedding
  const embedding = await model.run(input, {
    mean_pool: true,
    normalize: true,
  })

  // Search similar documents
  const { data: documents } = await supabase.rpc('match_documents', {
    query_embedding: embedding,
    match_threshold: 0.78,
    match_count: 10,
  })

  return new Response(JSON.stringify({ documents }), {
    headers: { 'Content-Type': 'application/json' }
  })
})
```

</details>

---

## Database Schema Patterns

<details>
<summary>User Profiles</summary>

```sql
-- User profiles table
CREATE TABLE profiles (
  id UUID REFERENCES auth.users NOT NULL,
  updated_at TIMESTAMP WITH TIME ZONE,
  username TEXT UNIQUE,
  avatar_url TEXT,
  website TEXT,
)
```

</details>
