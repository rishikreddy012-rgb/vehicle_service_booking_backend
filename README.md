# Vehicle Service Booking Backend

Spring Boot 3 REST API. This is a Java service; a Vercel deployment may show Ready without running Spring Boot, resulting in a 404.

## Deploy on Render

Create a Web Service from this repository on branch fix/render-java-backend, select Docker, then deploy. The included Dockerfile builds and runs the application.

Set these variables in Render. Enter database credentials directly in the Render dashboard; never commit them here.

| Variable | Value |
| --- | --- |
| DB_URL | JDBC URL to existing MySQL, e.g. jdbc:mysql://HOST:3306/vehicle_service?serverTimezone=UTC |
| DB_USERNAME | MySQL username |
| DB_PASSWORD | MySQL password |
| JWT_SECRET | Random secret of at least 32 bytes |
| CORS_ORIGIN | Exact frontend origins, comma-separated, no trailing slash |

The service listens on Render's PORT. Verify https://YOUR-RENDER-HOST/api/health returns {"status":"UP"}. The database must be reachable and the Flyway migration must succeed at startup.

## Connect the frontend

In the frontend Vercel project set VITE_API_BASE_URL to https://YOUR-RENDER-HOST/api for Production (and Preview if needed), then redeploy. Set CORS_ORIGIN to the exact frontend domain(s). Vite embeds this setting during build.

## Local development

Requirements: Java 21 and MySQL. Set DB_URL, DB_USERNAME, DB_PASSWORD, and a 32+ byte JWT_SECRET, then run ./mvnw spring-boot:run. CORS defaults to http://localhost:5173.
