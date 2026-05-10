# Google OAuth Setup Guide

## Step 1: Create Google OAuth Credentials

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select existing one
3. Navigate to **APIs & Services** → **Credentials**
4. Click **+ Create Credentials** → **OAuth 2.0 Client IDs**
5. If prompted, configure the OAuth consent screen first:
   - Choose "External" user type
   - Fill in app name, user support email, and developer contact
   - Add scopes: `email`, `profile`, `openid`
6. For Application type, select **Web application**
7. Add Authorized JavaScript origins:
   - `http://localhost:3000` (development)
   - `https://yourdomain.com` (production)
8. Add Authorized redirect URIs:
   - `https://gmbwakucarzkcxqkjnoz.supabase.co/auth/v1/callback` (Supabase)
   - For local dev, also add: `http://localhost:3000/auth/callback`
9. Copy the **Client ID** and **Client Secret**

## Step 2: Configure in Supabase

1. Go to [Supabase Dashboard](https://app.supabase.com/)
2. Select your project
3. Navigate to **Authentication** → **Providers**
4. Enable **Google** provider
5. Paste your Google **Client ID** and **Client Secret**
6. Save

## Step 3: Verify Redirect URI in Supabase

1. In Supabase, go to **Authentication** → **URL Configuration**
2. Verify your Site URL is set correctly:
   - Development: `http://localhost:3000`
   - Production: `https://yourdomain.com`

## Step 4: Test

1. Run `npm run dev` locally
2. Navigate to `http://localhost:3000/login`
3. Click "Continue with Google"
4. Sign in with a test Google account
5. Should redirect to dashboard or onboarding

## Environment Variables

No additional env vars needed for Google OAuth — Supabase handles it automatically using the credentials configured in the dashboard.

## Troubleshooting

- **Redirect URI mismatch**: Ensure the redirect URI in Google Console exactly matches Supabase's OAuth callback URL
- **Invalid client ID**: Double-check credentials in Supabase are correct
- **CORS errors**: Make sure authorized origins are set in Google Console
- **Callback loop**: Check that `/auth/callback` route exists and redirects properly

## Testing with Local Emails

For development, you can still use email/password login with test accounts created in Supabase:

1. Go to Supabase Dashboard → Authentication → Users
2. Create a test user with email & password
3. Use those credentials on `/login` page
