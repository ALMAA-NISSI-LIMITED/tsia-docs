# Environment Variable Reference

Complete reference for every variable in `.env`. Copy `.env.example` to `.env` and fill in the values below.

---

## Application

| Variable | Default | Description |
|---|---|---|
| `APP_NAME` | `Laravel` | Display name used in emails and UI. Set to `SafiRides`. |
| `APP_ENV` | `production` | Runtime environment. Use `local` for dev, `production` for prod. |
| `APP_KEY` | _(empty)_ | 32-byte encryption key. **Generate once:** `php artisan key:generate`. Never share or rotate in prod without a plan. |
| `APP_DEBUG` | `false` | Set `true` locally to show stack traces in the browser. **Must be `false` in production** — leaks internals. |
| `APP_URL` | `http://localhost` | Full public URL including scheme. Used for asset URLs, email links, and CORS. E.g. `https://admin.safirides.net`. |
| `APP_DEMO` | `false` | Enables demo mode (restricts destructive admin actions). Leave `false` unless running a public demo instance. |

---

## Logging

| Variable | Default | Description |
|---|---|---|
| `LOG_CHANNEL` | `daily` | Laravel log driver. `daily` rotates logs by date under `storage/logs/`. Options: `single`, `daily`, `stderr`, `stack`. |
| `LOG_LEVEL` | `debug` | Minimum severity to log. Use `debug` locally, `warning` or `error` in prod to reduce noise. |
| `LOG_API_PAYLOADS` | `false` | Log full API request/response bodies (sensitive fields are masked). Enable briefly for debugging; leave off in prod. |

---

## Database

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `DB_CONNECTION` | `mysql` | Driver. Always `mysql` for this project. | — |
| `DB_HOST` | `127.0.0.1` | MySQL hostname. Use `db` when running in Docker Compose. | — |
| `DB_PORT` | `3306` | MySQL port. Docker Compose maps to `3307` on the host. | — |
| `DB_DATABASE` | `laravel` | Database name. Set to `safirides`. | Create via `mysql -e "CREATE DATABASE safirides;"` |
| `DB_USERNAME` | `root` | Database user. | Your MySQL setup |
| `DB_PASSWORD` | _(empty)_ | Database password. | Your MySQL setup |

---

## Cache, Queue & Session

| Variable | Default | Description |
|---|---|---|
| `CACHE_DRIVER` | `redis` | Cache backend. Use `redis` in prod and Docker. Use `array` for tests. |
| `QUEUE_CONNECTION` | `redis` | Queue driver. Use `redis` in prod (2× Supervisor workers). Use `sync` locally if you don't want a separate worker process. |
| `SESSION_DRIVER` | `file` | Admin dashboard session storage. `file` is fine for single-server; use `redis` for multi-server. |
| `SESSION_LIFETIME` | `120` | Admin session length in minutes before idle logout. The `SessionTimeout` middleware enforces a 30 min idle timeout independently. |
| `SESSION_EXPIRE_ON_CLOSE` | `true` | Destroys the admin session when the browser closes. |

---

## Redis

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `REDIS_HOST` | `127.0.0.1` | Redis hostname. Use `redis` in Docker Compose. | — |
| `REDIS_PASSWORD` | `null` | Redis auth password. Leave `null` if no auth configured. | Your Redis setup |
| `REDIS_PORT` | `6379` | Redis port. Docker Compose maps to `6380` on the host. | — |

> **Note:** Redis DB 2 is shared with the Node.js realtime gateway on the `shared` connection. Do not add a key prefix to that connection or it will break the gateway.

---

## Internal API

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `INTERNAL_API_KEY` | `change-me-to-a-strong-secret` | Shared secret for the `/internal` route layer used by the Node.js gateway. Must match `INTERNAL_API_KEY` in the Node gateway's env. | Generate with `openssl rand -hex 32` |

---

## Mail

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `MAIL_MAILER` | `smtp` | Mail driver. Options: `smtp`, `sendmail`, `log` (dev), `array` (tests). | — |
| `MAIL_HOST` | `mailhog` | SMTP server hostname. | Your email provider (e.g. `smtp.gmail.com`, `smtp.sendgrid.net`) |
| `MAIL_PORT` | `1025` | SMTP port. Common: `587` (TLS), `465` (SSL), `25`. | Your email provider |
| `MAIL_USERNAME` | _(empty)_ | SMTP login username. | Your email provider |
| `MAIL_PASSWORD` | _(empty)_ | SMTP login password or API key. | Your email provider |
| `MAIL_ENCRYPTION` | _(empty)_ | Encryption: `tls`, `ssl`, or blank. | Your email provider |
| `MAIL_FROM_ADDRESS` | _(empty)_ | Sender address for all outgoing mail. E.g. `no-reply@safirides.net`. | Your domain |
| `MAIL_FROM_NAME` | `${APP_NAME}` | Sender display name. Defaults to `APP_NAME`. | — |

---

## File Storage

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `FILESYSTEM_DRIVER` | `local` | Default storage disk for file uploads. `local` stores under `storage/app/`. | — |
| `CMS_IMAGE_DISK` | `public` | Disk used for CMS images (articles, promos, etc.). Set to `s3` to offload to AWS S3 — requires the AWS vars below. | — |
| `AWS_ACCESS_KEY_ID` | _(empty)_ | AWS IAM access key. Only needed if `CMS_IMAGE_DISK=s3`. | [AWS IAM Console](https://console.aws.amazon.com/iam/) → Users → Security credentials |
| `AWS_SECRET_ACCESS_KEY` | _(empty)_ | AWS IAM secret. Paired with the access key above. | AWS IAM Console (shown once at creation) |
| `AWS_DEFAULT_REGION` | `us-east-1` | AWS region for the S3 bucket. | Your S3 bucket's region |
| `AWS_BUCKET` | _(empty)_ | S3 bucket name. | [AWS S3 Console](https://s3.console.aws.amazon.com/) |

---

## Google Maps

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `GOOGLE_MAP_KEY` | _(empty)_ | Google Maps API key used for `get_route_distance_and_duration()` — every ride fare calculation depends on this. | [Google Cloud Console](https://console.cloud.google.com/) → APIs & Services → Credentials → Create API Key. Enable **Directions API** and **Distance Matrix API**. |

---

## Push Notifications — OneSignal

OneSignal sends the **visible** push notifications to riders and drivers. There are two separate OneSignal apps (one per mobile app).

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `IS_ONESIGNAL` | `0` | Master toggle. Set `1` to enable OneSignal push. | — |
| `ONESIGNAL_APP_ID` | _(empty)_ | OneSignal App ID for the **rider** app. | [OneSignal Dashboard](https://app.onesignal.com/) → Your rider app → Settings → Keys & IDs |
| `ONESIGNAL_REST_API_KEY` | _(empty)_ | REST API key for the rider app. | Same page as above |
| `ONESIGNAL_DRIVER_APP_ID` | _(empty)_ | OneSignal App ID for the **driver** app. | OneSignal Dashboard → Your driver app → Settings → Keys & IDs |
| `ONESIGNAL_DRIVER_REST_API_KEY` | _(empty)_ | REST API key for the driver app. | Same page as above |

---

## Push Notifications — Firebase (FCM)

Firebase sends **data-only** (silent) messages to drivers so `onMessageReceived()` fires even when the app is closed (ride ringing). Also used for Firestore.

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `FIREBASE_SERVER_KEY` | _(empty)_ | Legacy FCM server key (used as fallback). | [Firebase Console](https://console.firebase.google.com/) → Project Settings → Cloud Messaging → Server key |
| `FIREBASE_CREDENTIALS` | `/path/to/firebase-service-account.json` | **Absolute path** to the Firebase service account JSON file. Required for FCM v1 API and Firestore. | Firebase Console → Project Settings → Service Accounts → Generate new private key. Save the downloaded JSON on your server and set the path here. |
| `FIREBASE_DATABASE_URL` | _(empty)_ | Firebase Realtime Database URL (if used). Format: `https://your-project.firebaseio.com`. | Firebase Console → Realtime Database |

---

## MQTT (Real-time Mobile Updates)

MQTT pushes live ride status updates to the mobile apps.

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `MQTT_HOST` | `""` | Hostname of your MQTT broker. E.g. `broker.hivemq.com` or a self-hosted Mosquitto instance. | Your MQTT broker setup |
| `MQTT_PORT` | `1883` | MQTT port. Use `8883` for TLS. | Your broker config |
| `MQTT_ENABLE_LOGGING` | `false` | Log all MQTT publish calls. Enable for debugging connection issues. | — |
| `MQTT_UNIQUE_TOPIC_NAME` | _(empty)_ | Prefix for all MQTT topics. E.g. `safirides_prod`. Must match the mobile app config. | Choose a unique string per environment |

---

## M-Pesa Payments

M-Pesa is used for rider STK push payments and B2C driver payouts. Credentials are managed through a wrapper service, not directly via Safaricom.

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `MPESA_BASE_URL` | `https://mpesa-wrapper.onrender.com` | Base URL of the M-Pesa wrapper service. Change to your own wrapper URL in production. | Your M-Pesa wrapper deployment |
| `MPESA_APP_ID` | _(empty)_ | App ID issued by the M-Pesa wrapper. | Your wrapper service admin |
| `MPESA_CALLBACK_URL` | _(empty)_ | Public HTTPS URL where Safaricom posts payment results. E.g. `https://admin.safirides.net/api/mpesa/callback`. Must be publicly reachable (no localhost). | Your server's public URL |
| `MPESA_CALLBACK_SECRET` | _(empty)_ | HMAC secret used to verify incoming M-Pesa callbacks. | Generate with `openssl rand -hex 32` and configure the same value in the wrapper |
| `MPESA_REQUIRE_CALLBACK_SIGNATURE` | `true` | Reject callbacks whose HMAC signature doesn't match. Set `false` only during local testing with a tunnel. | — |
| `MPESA_TRUSTED_IPS` | _(empty)_ | Comma-separated list of Safaricom IP ranges to whitelist for callbacks. Leave blank to skip IP filtering. | [Safaricom Developer Portal](https://developer.safaricom.co.ke/) |

> **Note:** Paystack card credentials (test/live keys) are stored in the **`payment_gateways` database table**, not in `.env`. Toggle between test and live mode in the admin dashboard.

---

## SMS (OTP Delivery)

SMS delivers the 6-digit OTP during mobile login. Three providers are supported; only one is active at a time.

| Variable | Default | Description |
|---|---|---|
| `SMS_ENABLED` | `false` | Master toggle. Set `true` to send real SMS. Leave `false` locally to skip SMS and use email fallback. |
| `SMS_PROVIDER` | `africas_talking` | Active provider. Options: `africas_talking`, `twilio`, `infobip`. |
| `SMS_DEFAULT_COUNTRY_CODE` | `+254` | Default country code prepended to numbers without one. Kenya = `+254`. |
| `SMS_CONNECT_TIMEOUT_SECONDS` | `3` | HTTP connection timeout when calling the SMS provider. |
| `SMS_TIMEOUT_SECONDS` | `10` | Total request timeout. |
| `SMS_RETRY_TIMES` | `1` | Number of retries on failure before giving up. |
| `SMS_RETRY_DELAY_MS` | `200` | Delay between retries in milliseconds. |

### Africa's Talking (default provider)

| Variable | Description | Where to get |
|---|---|---|
| `AFRICAS_TALKING_USERNAME` | Your Africa's Talking account username. Use `sandbox` for testing. | [Africa's Talking Dashboard](https://account.africastalking.com/) → Settings |
| `AFRICAS_TALKING_API_KEY` | API key for your account or sandbox. | Africa's Talking Dashboard → Settings → API Key |
| `AFRICAS_TALKING_SHORTCODE` | Sender ID or shortcode for outgoing SMS. E.g. `SafiRides`. | Africa's Talking Dashboard → SMS → Shortcodes |

### Twilio (alternative)

| Variable | Description | Where to get |
|---|---|---|
| `TWILIO_SID` | Twilio Account SID. | [Twilio Console](https://console.twilio.com/) → Account Info |
| `TWILIO_TOKEN` | Twilio Auth Token. | Twilio Console → Account Info |
| `TWILIO_FROM` | Twilio phone number to send from. E.g. `+12025550100`. | Twilio Console → Phone Numbers |

### Infobip (alternative)

| Variable | Description | Where to get |
|---|---|---|
| `INFOBIP_API_KEY` | Infobip API key. | [Infobip Portal](https://portal.infobip.com/) → Developer Tools → API Keys |
| `INFOBIP_BASE_URL` | Your Infobip base URL. Format: `https://xxxxx.api.infobip.com`. | Infobip Portal → shown on the API key page |
| `INFOBIP_SENDER` | Sender name or number. Defaults to `SafiRides`. | Infobip Portal → Numbers |

---

## Authentication & Security

| Variable | Default | Description |
|---|---|---|
| `SANCTUM_EXPIRATION` | `120` | Mobile API token lifetime in minutes. `null` = never expires. |
| `SANCTUM_STATEFUL_DOMAINS` | _(computed)_ | Comma-separated domains allowed to use cookie-based Sanctum auth (admin dashboard SPA). Defaults to `APP_URL` host. |
| `CORS_ALLOWED_ORIGINS` | `http://localhost:3000` | Comma-separated origins allowed to make cross-origin API requests. Set to your mobile app's web origin or `*` for open APIs. |
| `CORS_SUPPORTS_CREDENTIALS` | `true` | Allow cookies/auth headers in CORS requests. Required for the admin dashboard. |
| `TRUSTED_PROXIES` | `127.0.0.1` | Comma-separated IPs whose `X-Forwarded-*` headers Laravel trusts. Set `127.0.0.1` when Nginx is on the same host. Set `*` only if PHP is not publicly exposed. |
| `MOBILE_LOGIN_REQUIRE_FIREBASE_TOKEN` | `false` | Require a valid Firebase ID token alongside the OTP on mobile login. Adds a second factor. |

### OTP Configuration

| Variable | Default | Description |
|---|---|---|
| `AUTH_OTP_ENFORCED` | `false` | Require OTP on every login. Set `true` in production. |
| `AUTH_OTP_ENFORCEMENT_MODE` | `compatible` | `compatible` = accept logins without OTP if the client doesn't send one. `strict` = always require OTP. |
| `AUTH_OTP_FALLBACK_TO_EMAIL_WHEN_SMS_UNAVAILABLE` | `true` | Fall back to email OTP if SMS fails. |
| `AUTH_OTP_LENGTH` | `6` | OTP digit length. |
| `AUTH_OTP_EXPIRY_MINUTES` | `5` | OTP validity window in minutes. |
| `AUTH_OTP_MAX_ATTEMPTS` | `5` | Failed attempts before the OTP is invalidated. |
| `AUTH_OTP_MAX_RESENDS` | `3` | Maximum resend requests per OTP. |
| `AUTH_OTP_RESEND_COOLDOWN_SECONDS` | `30` | Minimum seconds between resend requests. |
| `AUTH_OTP_RATE_LIMIT_PER_15_MIN` | `10` | Maximum OTP requests per phone number per 15 minutes. |

---

## Surge Pricing

| Variable | Default | Description | Where to get |
|---|---|---|---|
| `OPENWEATHERMAP_API_KEY` | _(empty)_ | API key for live weather data used in surge calculations (rain/storms raise multiplier). | [OpenWeatherMap](https://openweathermap.org/api) → Sign up → API Keys. Free tier covers this. |
| `SURGE_MAX_MULTIPLIER` | `2.00` | Hard cap on the surge multiplier. `2.00` = fares can at most double. Stored as a float. |
| `SURGE_CRON_INTERVAL_MINUTES` | `3` | How often the surge recalculation job runs. |
| `SURGE_DEMAND_WINDOW_MINUTES` | `15` | Rolling window for counting ride requests when calculating demand. |
| `SURGE_SPIKE_THRESHOLD` | `5` | Minimum ride requests in `SURGE_SPIKE_WINDOW_MINUTES` to trigger a demand spike. |
| `SURGE_SPIKE_WINDOW_MINUTES` | `2` | Short window used to detect sudden spikes. |
| `SURGE_RAMPDOWN_STEP` | `0.10` | Amount the multiplier decreases each cycle when demand falls. |
| `SURGE_HOTSPOT_MIN_REQUESTS` | `8` | Minimum requests within `SURGE_HOTSPOT_RADIUS_KM` to flag a hotspot. |
| `SURGE_HOTSPOT_RADIUS_KM` | `2` | Radius in km for hotspot detection clustering. |
| `SURGE_WEATHER_CACHE_MINUTES` | `15` | How long to cache weather data before fetching fresh data. |
| `SURGE_WEATHER_STALE_MINUTES` | `30` | After this many minutes without a refresh, weather data is considered stale and ignored. |
| `SURGE_EXPIRES_AFTER_MINUTES` | `10` | Surge zone expires automatically after this many minutes with no recalculation. |

---

## Pusher (optional)

Not actively used — present for compatibility with Laravel's default broadcast scaffolding. Only needed if you switch `BROADCAST_DRIVER=pusher`.

| Variable | Default |
|---|---|
| `PUSHER_APP_ID` | _(empty)_ |
| `PUSHER_APP_KEY` | _(empty)_ |
| `PUSHER_APP_SECRET` | _(empty)_ |
| `PUSHER_APP_CLUSTER` | `mt1` |

---

## Quick-start checklist

Minimum vars to get the app running locally:

- [x] `APP_KEY` — run `php artisan key:generate`
- [x] `DB_*` — point at your MySQL instance
- [x] `REDIS_HOST` — point at Redis
- [x] `INTERNAL_API_KEY` — any strong secret
- [ ] `GOOGLE_MAP_KEY` — needed for fare calculations
- [ ] `FIREBASE_CREDENTIALS` — needed for driver push notifications
- [ ] `MPESA_BASE_URL` + `MPESA_APP_ID` + `MPESA_CALLBACK_URL` — needed for payments
- [ ] `SMS_ENABLED=true` + one SMS provider — needed for OTP login on mobile
- [ ] `IS_ONESIGNAL=1` + both OneSignal key pairs — needed for rider/driver visible notifications
- [ ] `OPENWEATHERMAP_API_KEY` — needed for weather-based surge pricing
