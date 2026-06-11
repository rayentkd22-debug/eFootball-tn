eFootball Arena - Supabase Setup Guide
======================================

1. SUPABASE SETUP
-----------------
1. Go to https://app.supabase.com
2. Open your project: zpfdtqitcfcuzqhygmys
3. Go to SQL Editor
4. Run this SQL to create tables:

CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  email TEXT UNIQUE NOT NULL,
  password TEXT NOT NULL,
  whatsapp TEXT,
  country TEXT,
  points INTEGER DEFAULT 0,
  wins INTEGER DEFAULT 0,
  losses INTEGER DEFAULT 0,
  goals INTEGER DEFAULT 0,
  rank TEXT DEFAULT 'Bronze',
  verified BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE tournaments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  description TEXT,
  max_players INTEGER DEFAULT 16,
  players UUID[] DEFAULT '{}',
  status TEXT DEFAULT 'open',
  start_date TIMESTAMP,
  bracket JSONB DEFAULT '[]',
  created_by UUID REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE messages (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sender_id UUID REFERENCES users(id),
  receiver_id UUID REFERENCES users(id),
  text TEXT NOT NULL,
  read BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE matches (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  p1_id UUID REFERENCES users(id),
  p2_id UUID REFERENCES users(id),
  p1_score INTEGER,
  p2_score INTEGER,
  type TEXT DEFAULT 'friendly',
  created_at TIMESTAMP DEFAULT NOW()
);

5. Go to Project Settings > API
6. Copy your NEW anon key
7. Open the HTML file
8. Find: const SUPABASE_KEY = 'YOUR_SUPABASE_KEY_HERE';
9. Replace with your new key

2. IMPORTANT SECURITY NOTE
----------------------------
- This is Option A (key in code) - less secure
- For better security, use Option B (Edge Functions)
- Never share your key publicly
- Regenerate key if exposed

3. DEMO USERS
-------------
You can create demo users via Supabase Table Editor
or let users register normally.

4. FEATURES
-----------
✅ Real user registration/login
✅ Tournaments (create, join, view)
✅ Friendly matches with score tracking
✅ Live leaderboard
✅ Messaging between players
✅ Rank system (Bronze → Champion)
✅ PWA support
✅ Works on all devices
