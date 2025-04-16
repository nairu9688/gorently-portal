# Implementation plan

## Phase 1: Environment Setup

1. **Prevalidation:** Check if the current directory is already a GoRently Portal project (e.g., look for existing project files like package.json or tsconfig.json). Reference: Project Overview.
2. **Starter Kit Initialization:** If not found, clone the CodeGuide Starter Pro Repo from [https://github.com/codeGuide-dev/codeguide-starter-pro](https://github.com/codeGuide-dev/codeguide-starter-pro) into a new project directory. Reference: Project Overview & CodeGuide Starter Pro Repo.
3. **Node.js Version Check:** Verify that Node.js v20.2.1 is installed by running `node -v`; if not, install Node.js v20.2.1. Reference: Tech Stack: Core Tools.
4. **Next.js Setup:** Ensure that Next.js v14 is installed (note: Next.js v14 is required for compatibility with current LLM tools). Reference: Tech Stack.
5. **Cursor Metrics Setup:** In the project root, create a `cursor_metrics.md` file. Reference: Environment Setup / Cursor.
6. **Cursor Directory Creation:** In the project root, create a `.cursor` directory if it doesn’t already exist. Reference: Environment Setup / Cursor.
7. **MCP Configuration (Cursor):** Inside the `.cursor` directory, create a file named `mcp.json` if it doesn’t exist. Open this file for editing. Reference: Environment Setup / Cursor.
8. **MCP Config Setup for macOS and Windows:** Insert the following configuration into `.cursor/mcp.json` (choose the version that matches your OS):

   - For macOS:
     ```json
     { "mcpServers": { "supabase": { "command": "npx", "args": ["-y", "@modelcontextprotocol/server-postgres", "<connection-string>"] } } }
     ```

   - For Windows:
     ```json
     { "mcpServers": { "supabase": { "command": "cmd", "args": ["/c", "npx", "-y", "@modelcontextprotocol/server-postgres", "<connection-string>"] } } }
     ```

   Reference: Environment Setup / Cursor.
9. **Display Supabase Connection Link:** Provide the link `https://supabase.com/docs/guides/getting-started/mcp#connect-to-supabase-using-mcp` so that the user can obtain the Supabase connection string. Reference: Environment Setup / Cursor.
10. **User Action:** Once the connection string is provided by the user, replace `<connection-string>` in the `.cursor/mcp.json` file accordingly. Reference: Environment Setup / Cursor.
11. **MCP Connection Validation:** Navigate to Settings/MCP in Cursor to verify a green active status, confirming the backend server connection. Reference: Environment Setup / Cursor.

## Phase 2: Frontend Development

12. **Project Dependency Installation:** In the project root, install project dependencies using `npm install` (ensuring integration of Next.js v14, Tailwind CSS, Typescript, and Shadcn UI). Reference: Tech Stack.
13. **Tailwind CSS Setup:** Configure Tailwind CSS by creating and updating `tailwind.config.js` and including Tailwind in the global CSS file (e.g., `/styles/globals.css`). Reference: Tech Stack & Overall Design.
14. **Setting up Shadcn UI:** Install and configure Shadcn UI components. Reference: Tech Stack.
15. **Administrator Dashboard Page:** Create an Administrator dashboard page at `/pages/admin/dashboard.tsx` that lists subscribers, monitors service usage, and displays analytics. Reference: User Interfaces: Administrator Interface.
16. **Host Online Check-In Form Builder:** Create a Host interface page at `/pages/host/checkin-builder.tsx` and implement a form builder supporting various field types (text, numeric, single/multiple choice, file upload). Reference: User Interfaces: Host Interface.
17. **Custom Field Validations:** In the check-in form builder, implement custom field validations (regex, conditional logic) using Typescript client-side code. Reference: User Interfaces: Host Interface.
18. **Host Customization Settings:** Create a settings page at `/pages/host/customize.tsx` for brand personalization. Apply the specific colors (`#2383f4`, `#2d323e`, `#1e232d`, `#f1f1f1`) and fonts (Plus Jakarta Sans and Montserrat). Reference: User Interfaces: Host Interface.
19. **Digital Guide Builder:** Create a Guide Builder page at `/pages/host/guide-builder.tsx` that allows hosts to build rich content guides (integrating text, images, links, emojis, and titles) and generates property pages with QR codes. Reference: User Interfaces: Host Interface.
20. **Upsell Services Management Interface:** Create an Upsell Services management page at `/pages/host/upsell.tsx` to manage fixed, request-based, and custom upsell services, including pricing adjustments. Reference: User Interfaces: Host Interface.
21. **Guest Online Pre-Check-In Page:** Create a Guest interface page at `/pages/guest/pre-checkin.tsx` presenting a guided form for online pre-check-in. Reference: User Interfaces: Guest Interface.
22. **Digital Guide and Upsell Display for Guests:** Create a Guest digital guide page at `/pages/guest/digital-guide.tsx` that presents property details, upsell services, and dynamic guide content. Reference: User Interfaces: Guest Interface.
23. **Frontend API Service Layer:** Inside `/services/api.ts`, build API service functions (using Axios or built-in fetch) to communicate with backend endpoints (Guesty API updates, Stripe payments, Twilio notifications). Reference: Integration with External Systems.
24. **Testing Frontend Components:** After coding each UI component, execute frontend tests (e.g., `npm run test`) to validate functionality and responsiveness. Reference: Overall Design & User Interfaces.

## Phase 3: Backend Development

25. **Supabase Database Setup:** Set up Supabase for the backend. Create the required PostgreSQL schema which includes tables for users, reservations, upsell_services, custom_fields, and notifications. Reference: Additional Requirements & Integration with External Systems.
26. **Clerk Authentication Integration:** Configure Clerk Auth for user registration and session management by setting up endpoints (e.g., `/api/auth/register`, `/api/auth/login`). Reference: Tech Stack & User Management.
27. **Guesty API Integration (Retrieval):** Create an API endpoint at `/api/guesty/reservations` (GET) that retrieves real-time reservation data from the Guesty API using the provided Guesty Authentication Token. Reference: Integration with External Systems: Guesty API.
28. **Guesty API Integration (Update):** Create an API endpoint at `/api/guesty/reservations/[id]` (PUT) to update reservations with custom access links and sync check-in form fields to Guesty custom fields. Reference: Integration with External Systems: Guesty API.
29. **Stripe Integration:** Develop backend endpoints (e.g., `/api/payments/create` and `/api/payments/webhook`) to process payments for upsell services, ensuring a 2% commission is retained. Reference: Integration with External Systems: Stripe.
30. **Twilio WhatsApp Integration:** Set up an API endpoint at `/api/notifications/whatsapp` to send notifications for upsell requests and check-in events via Twilio’s WhatsApp service. Reference: Integration with External Systems: WhatsApp.
31. **Real-Time Data Sync Setup:** Implement a background job or webhook endpoint to periodically synchronize and refresh reservation data from Guesty API in real time. Reference: Additional Requirements: Real-time Data Synchronization.
32. **Backend Unit Testing:** Develop and run tests (e.g., using Jest) for each backend endpoint to ensure correct responses (status 200 and expected data). Reference: Quality Assurance Practices.

## Phase 4: Integration

33. **Connect Frontend to Backend:** In the frontend service layer (e.g., `/services/api.ts`), integrate API calls to link UI components (check-in form, upsell management, etc.) with the corresponding backend endpoints. Reference: App Flow: Integration.
34. **Form to Guesty Data Flow:** Update the Host Online Check-In Form Builder to send form data to the `/api/guesty/reservations/[id]` endpoint for transferring custom field values. Reference: User Interfaces: Host Interface & Integration with External Systems: Guesty API.
35. **Upsell Payment Workflow:** Integrate the upsell services management interface with the Stripe payment endpoint so that upsell service requests trigger the payment processing flow. Reference: User Interfaces: Host Interface & Integration with External Systems: Stripe.
36. **Clerk Authentication Integration on Frontend:** Ensure frontend pages invoke Clerk Auth API functions during sign-up, login, and session-check events. Reference: Tech Stack: Clerk Auth.
37. **Twilio Notification Integration:** Link backend Twilio notification endpoints to trigger WhatsApp messages upon upsell requests and check-in completions. Reference: Integration with External Systems: WhatsApp.
38. **Integration Testing:** Run end-to-end tests (e.g., using Cypress) to ensure communication flows correctly between frontend and backend APIs. Reference: Quality Assurance Practices.

## Phase 5: Deployment

39. **Environment Variables Setup:** Create a configuration file (e.g., `.env.local`) in the project root to store sensitive keys and tokens for Supabase, Clerk, Guesty API, Stripe, and Twilio. Reference: Tech Stack & Integration with External Systems.
40. **CI/CD Pipeline Configuration:** Set up CI/CD using GitHub Actions or an equivalent tool to build, test, and deploy the application automatically. Reference: Deployment.
41. **Deploy Supabase Backend:** Follow Supabase documentation to deploy the backend database schema and functions to your Supabase instance. Reference: Additional Requirements: Data Security.
42. **Deploy Next.js Frontend:** Deploy the Next.js frontend to a hosting platform (e.g., Vercel), ensuring Next.js v14 compatibility is maintained. Reference: Tech Stack: Next.js.
43. **Cloud Environment Verification:** After deployment, verify that all environment variables have been correctly set and that API endpoints are reachable. Reference: Deployment.
44. **User Acceptance Testing:** Conduct final testing of the full user flows (Administrator, Host, and Guest interfaces) on the live deployment by simulating reservation data fetch, payment, and notifications. Reference: Overall Design & User Interfaces.
45. **Monitoring & Logging Setup:** Implement logging (for example, via Supabase logging and a third-party tool) for Guesty API errors, payment mismatches, and other critical events, and ensure that notifications are displayed in the Administrator dashboard. Reference: Integration with External Systems: Guesty API.
46. **Post-Deployment Validation:** Run comprehensive tests using automated scripts (e.g., end-to-end tests with Cypress) to verify that real-time data synchronization and integrations (Clerk, Stripe, Twilio, Guesty) work seamlessly. Reference: Q&A: Pre-Launch Checklist.

---

This step-by-step plan fulfills the requirements for a full-stack implementation of the GoRently Portal, covering environment setup, frontend and backend development, seamless integration with external services, and deployment with CI/CD pipelines. Each step has been designed as a single action with references to the provided documents.