# Ad stack remote config

One JSON per app, fetched by every install at launch from
`https://ysharad.github.io/goapps/adconfig/<app>.json` (5s timeout, cached on
device, test-ID fallback baked into the APK). Editing a file here changes the
live ad behavior of that app on its next launch — no release needed.

## Fields
- `ads_enabled` — false collapses the ad slot entirely (kill switch)
- `mode` — which stack fills the banner slot:
  - `"admob"`  plain AdMob (`admob_banner_unit`)
  - `"gam"`    Google Ad Manager / AdX (`gam_banner_unit`, `/network/unit` path)
  - `"prebid"` Prebid Mobile header bidding rendered through GAM (`prebid.*`)
- `prebid.server_url` — Prebid Server auction endpoint
- `prebid.account_id` — Prebid Server account
- `prebid.banner_config_id` — stored imp/config id for the banner
- `prebid.gam_ad_unit` — GAM ad unit the Prebid targeting is sent to
- `prebid.width`/`height` — banner size for the Prebid auction

All files currently point at Google's and Prebid's public TEST ids.
To go live for an app: create the AdMob/GAM unit, edit that app's JSON, done.
(The AdMob APPLICATION_ID in each app's manifest is the only thing that
still requires an app release to change.)
