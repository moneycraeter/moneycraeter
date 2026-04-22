# CHROMAWIN — Setup Guide

## 1. Supabase Setup

### Create project at supabase.com, then run this SQL:

```sql
-- profiles table (extends auth.users)
create table profiles (
  id uuid references auth.users(id) primary key,
  name text,
  email text,
  phone text,
  balance numeric default 0,
  created_at timestamptz default now()
);

-- bets table
create table bets (
  id bigserial primary key,
  user_id uuid references auth.users(id),
  round_id integer,
  color text,
  amount numeric,
  multiplier integer,
  status text default 'pending',   -- pending | win | lose
  payout numeric default 0,
  created_at timestamptz default now()
);

-- transactions table
create table transactions (
  id bigserial primary key,
  user_id uuid references auth.users(id),
  amount numeric,
  type text,                        -- deposit | withdrawal | win | bet
  payment_id text,
  status text default 'success',
  created_at timestamptz default now()
);

-- Enable Row Level Security
alter table profiles enable row level security;
alter table bets enable row level security;
alter table transactions enable row level security;

-- Policies
create policy "Users can view own profile" on profiles for select using (auth.uid() = id);
create policy "Users can update own profile" on profiles for update using (auth.uid() = id);
create policy "Users can insert own profile" on profiles for insert with check (auth.uid() = id);

create policy "Users can view own bets" on bets for select using (auth.uid() = user_id);
create policy "Users can insert own bets" on bets for insert with check (auth.uid() = user_id);
create policy "Users can update own bets" on bets for update using (auth.uid() = user_id);

create policy "Users can view own transactions" on transactions for select using (auth.uid() = user_id);
create policy "Users can insert own transactions" on transactions for insert with check (auth.uid() = user_id);
```

### Get your keys from: Settings → API
- `Project URL` → SUPABASE_URL
- `anon public` key → SUPABASE_KEY

---

## 2. Razorpay Setup

1. Create account at razorpay.com
2. Go to Settings → API Keys → Generate Test Key
3. Copy `Key ID` → RZP_KEY_ID (starts with `rzp_test_`)
4. For production: use `rzp_live_` key + verify payments server-side

---

## 3. Configure index.html

Replace these 3 constants at the top of the `<script>`:

```js
const SUPABASE_URL = 'https://xxxx.supabase.co';
const SUPABASE_KEY = 'eyJ...your-anon-key...';
const RZP_KEY_ID   = 'rzp_test_xxxxxxxxxxxx';
```

---

## 4. Production Checklist

- [ ] Verify Razorpay payments server-side (create a backend endpoint)
- [ ] Add email verification in Supabase Auth settings
- [ ] Set up Supabase Auth redirect URLs
- [ ] Enable rate limiting on bet placement
- [ ] Add server-side round result generation (replace client-side random)
- [ ] Host on Vercel / Netlify / any static host
- [ ] Add responsible gambling limits (daily loss limits etc.)
- [ ] Comply with local gambling regulations

---

## 5. Color Multipliers

| Color  | Multiplier | Win Probability |
|--------|-----------|-----------------|
| RED    | 2×        | 35%             |
| GREEN  | 3×        | 28%             |
| BLUE   | 4×        | 18%             |
| VIOLET | 5×        | 12%             |
| AMBER  | 6×        | 7%              |
