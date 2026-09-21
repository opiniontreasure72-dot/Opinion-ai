# Happy Chat + Opinion 2.0

Happy Chat is the social website. Opinion is the AI assistant built into it.

## Included
- Firebase Authentication, Firestore and Storage structure preserved.
- Opinion secure Vercel API endpoints.
- Real AI chat through the OpenAI Responses API.
- Web search tool support.
- Image understanding.
- Document/file input (including PDF/data files supported by the API).
- Voice input through supported browser speech recognition.
- Text-to-speech playback (browser speech first; server TTS endpoint available).
- Image generation endpoint.
- Conversation history in the browser.
- No OpenAI secret key in frontend code.

## Vercel environment variables

Add these in Vercel Project Settings → Environment Variables:

Required:
- `OPENAI_API_KEY` — your server-side OpenAI API key.
- `FIREBASE_SERVICE_ACCOUNT_JSON` — Firebase Admin service-account JSON as one-line JSON.

Optional:
- `OPENAI_MODEL` — defaults to `gpt-5.6-luna`.
- `OPENAI_IMAGE_MODEL` — defaults to `gpt-image-2`.
- `OPENAI_TTS_MODEL` — defaults to `gpt-4o-mini-tts`.
- `OPENAI_TTS_VOICE` — defaults to `alloy`.
- `ALLOWED_ORIGIN` — only needed if a different domain calls the API (comma-separated). Leave unset for same-site use.

Do NOT put any of these secret values into `index.html`.

## Firebase setup
The existing Firebase web configuration is kept in `index.html`. Firebase web config is not a secret; Firestore/Storage rules and server authentication provide the protection.

The Vercel backend verifies the signed-in user's Firebase ID token when `FIREBASE_SERVICE_ACCOUNT_JSON` is configured.

## Deploy
1. Upload/push this folder to the GitHub repository used by Vercel, or import the folder into Vercel.
2. Add the environment variables above.
3. Deploy.
4. Open Happy Chat, sign in, open Opinion, and test text, web search, image/file attachment, voice input, and read-aloud.

## Security
All `/api/*` endpoints (`chat`, `speak`, `image`) require a signed-in Firebase user and are lightly rate-limited per user. The rate limit is in-memory per server instance, so use Vercel KV/Upstash for a strict global cap before public launch. Set a monthly spend limit in your OpenAI account too.

Deploy rules with `firebase deploy --only firestore:rules,storage`.

## Important
AI features consume provider resources and may incur API charges. Keep the OpenAI key server-side and review your provider usage limits before public launch.
