services:
  oauth2-proxy:
    image: quay.io/oauth2-proxy/oauth2-proxy
    restart: always
    command:
      - "--provider=oidc"
      - "--oidc-issuer-url=https://onevarsity.in"
      - "--client-id=mastodon-client"
      - "--client-secret=mastodon-secret"
      - "--cookie-secret=random-secret"
      - "--cookie-secure=true"
      - "--cookie-domain=.onevarsity.in"
      - "--upstream=http://mastodon:3000"
      - "--upstream=http://moodle:80"
      - "--pass-authorization-header=true"
      - "--pass-user-headers=true"
    ports:
      - "4180:4180"
    environment:
      OAUTH2_PROXY_COOKIE_SECRET: "randomly-generated-key"
      OAUTH2_PROXY_CLIENT_ID: "mastodon-client"
      OAUTH2_PROXY_CLIENT_SECRET: "mastodon-secret"
