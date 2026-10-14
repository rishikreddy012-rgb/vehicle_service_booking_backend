# Vehicle Service Booking Backend

Spring Boot 3 REST API for the Vehicle Service Booking System.

## Live deployment

The production backend runs on Render and deploys from the `main` branch of this repository.

- **Render deployment:** [https://vehicle-service-booking-backend-qx8f.onrender.com](https://vehicle-service-booking-backend-qx8f.onrender.com)
- **API base URL:** [https://vehicle-service-booking-backend-qx8f.onrender.com](https://vehicle-service-booking-backend-qx8f.onrender.com)
- **Health check:** [https://vehicle-service-booking-backend-qx8f.onrender.com/api/health](https://vehicle-service-booking-backend-qx8f.onrender.com/api/health) — returns HTTP 200 when healthy.
- **Frontend:** [https://vehicle-service-booking-frontend-gold.vercel.app](https://vehicle-service-booking-frontend-gold.vercel.app)

Render's free web service may spin down when idle, so its first request after inactivity can take longer while it wakes.

## Render deployment setup

The Render web service is connected to this GitHub repository and tracks `main`. It uses the included `Dockerfile`. New commits to `main` are deployed by Render.

Configure these environment variables in the Render dashboard. Never commit database credentials or signing secrets to GitHub.

| Variable | Value |
| --- | --- |
| `DB_URL` | JDBC URL for the hosted MySQL database |
| `DB_USERNAME` | MySQL username |
| `DB_PASSWORD` | MySQL password |
| `JWT_SECRET` | Random secret of at least 32 bytes |
| `CORS_ORIGIN` | Exact frontend origin(s), comma-separated, without trailing slashes |

The app listens on Render's `PORT`. The database must be reachable and Flyway migrations must succeed during startup.

## Connect the frontend

Set `VITE_API_BASE_URL` in the Vercel project to `https://vehicle-service-booking-backend-qx8f.onrender.com/api`, then redeploy the frontend. Vite embeds this value during the build.

## Local development

Requirements: Java 21 and MySQL. Set `DB_URL`, `DB_USERNAME`, `DB_PASSWORD`, and a 32+ byte `JWT_SECRET`, then run `./mvnw spring-boot:run`. CORS defaults to `http://localhost:5173`.
