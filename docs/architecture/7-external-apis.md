# 7. External APIs

### API: Google Sign-In

*   **Purpose:** To allow users to register and log in to Recruitify using their existing Google account, providing a fast and secure authentication option.
*   **Documentation:** [https://developers.google.com/identity/sign-in/web/sign-in](https://developers.google.com/identity/sign-in/web/sign-in)
*   **Authentication:** OAuth 2.0. The frontend will handle the initial OAuth flow, receiving an ID Token from Google.
*   **Rate Limits:** N/A (Standard Google API usage policies apply).

**Key Endpoints Used:**

*   `POST https://oauth2.googleapis.com/tokeninfo?id_token={token}` - This endpoint will be called by our **API Service** to verify the integrity and authenticity of the ID Token received from the frontend.

**Integration Notes:**

*   A Google Cloud Platform project must be created and configured with the correct OAuth consent screen details.
*   A Client ID and Client Secret must be securely stored in our backend's environment variables.
*   The frontend will be responsible for managing the pop-up/redirect flow to get the user's consent and retrieve the token.

---


### API: LinkedIn Login

*   **Purpose:** To allow users to register and log in using their existing LinkedIn account, which is highly relevant for a professional recruiting platform.
*   **Documentation:** [https://learn.microsoft.com/en-us/linkedin/consumer/integrations/self-serve/sign-in-with-linkedin-v2](https://learn.microsoft.com/en-us/linkedin/consumer/integrations/self-serve/sign-in-with-linkedin-v2)
*   **Authentication:** OAuth 2.0. The flow is similar to Google's, where the frontend initiates the process and the backend verifies the user and retrieves their profile data.
*   **Rate Limits:** Standard LinkedIn API usage policies apply.

**Key Endpoints Used:**

*   `POST https://www.linkedin.com/oauth/v2/accessToken` - Our **API Service** will exchange an authorization code (provided by the frontend) for an access token.
*   `GET https://api.linkedin.com/v2/me` - Our **API Service** will use the access token to fetch basic profile information (like name and email) to create the user account.

**Integration Notes:**

*   A LinkedIn Developer Application must be created to obtain a Client ID and Client Secret.
*   The necessary permissions (scopes) like `r_liteprofile` and `r_emailaddress` must be requested.
*   Our backend will be responsible for securely handling the token exchange and fetching user data.

---
