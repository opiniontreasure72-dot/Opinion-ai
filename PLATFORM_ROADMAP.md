
# Happy Chat 3.1 Platform

The project now contains an integrated platform architecture for:

- Social feed: posts, reactions, comments, replies, shares and saves.
- Profiles: profile/cover/bio/follow relationships.
- Messaging: direct/group conversation UI contracts.
- Notifications: activity notification contract.
- Search: users/posts/hashtags contract.
- Stories: 24-hour content contract.
- Moderation: report/mute/block contracts.
- Admin: moderation and analytics extension point.
- Opinion: chat, web search, image/file input, voice and image-generation API endpoints.
- Mobile-first navigation and accessibility helpers.

## Production notes

Firebase Firestore/Storage rules remain the source of truth for database security.
The social layer now uses Firestore as its source of truth for profiles, follows, saved posts, notifications, moderation records and direct-message conversations. The existing feed, comments and public chat continue to use Firestore. Client-side actions remain constrained by Firestore rules; high-volume moderation and global rate limits should be moved to trusted backend infrastructure as usage grows.

Opinion secrets stay server-side in Vercel environment variables.

Required Opinion variables:
OPENAI_API_KEY
FIREBASE_SERVICE_ACCOUNT_JSON

Optional:
OPENAI_MODEL
OPENAI_IMAGE_MODEL
OPENAI_TTS_MODEL
OPENAI_TTS_VOICE
ALLOWED_ORIGIN

## Recommended deployment

1. Push this complete project to the GitHub repository connected to Vercel.
2. Add the environment variables in Vercel.
3. Deploy.
4. Configure Firebase Authentication providers.
5. Verify Firestore and Storage rules.
6. Test account creation, feed, messaging, uploads and Opinion on Android.
7. Only then make the site public.

## Important

A social platform needs server-side enforcement for moderation, rate limits and authorization.
Client-side JavaScript alone must never be treated as security.
