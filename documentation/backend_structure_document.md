# Backend Structure Document

This document explains the backend design, architecture, and infrastructure of the GoRently Portal project. The explanations are written in everyday language to make the concepts easy to understand for everyone.

## Backend Architecture

The backend is built around a modern and flexible structure to meet the project’s needs, ensuring it can grow and stay reliable over time. Here are the key points:

- **Frameworks and Tools Used:**
  - Supabase: Provides out-of-the-box backend services including a PostgreSQL database, storage, and edge functions.
  - Clerk Auth: Manages authentication and user management with advanced role setups like property manager and concierge.
  - Integration with APIs such as Guesty API for real-time data sync, Stripe for payments, and Twilio for WhatsApp notifications.
  - OpenAI is also available for any advanced AI-based features if needed.

- **Design Patterns: **
  - The project follows a modular structure with separation of concerns. This means that different parts of the backend (data management, authentication, API integrations) are kept separate. This makes it easier to update or change one section without affecting others.
  - The architecture supports scalability by using a serverless and cloud-based approach via Supabase. This means the backend can handle more user requests automatically by scaling resources up or down.
  - It also emphasizes maintainability by using standardized frameworks and clear API contracts so developers can easily understand and extend functionality over time.

## Database Management

Our data is stored and managed efficiently using Supabase's integrated PostgreSQL database. Here’s how it works:

- **Database Technology:**
  - **SQL Database:** We use PostgreSQL, which is known for handling complex queries and large-scale data reliably.

- **Data Handling:**
  - Information on users, form configurations, reservations, activity logs, and other data is stored in tables designed to handle both relational queries and fast read/writes.
  - Data is accessed through a combination of direct database queries and API endpoints, supported by Supabase's secure and fast data access layers.
  - Good practices include indexing data, using stored procedures for common tasks, and regularly backing up the database for data integrity.

## Database Schema

This section provides a human-readable overview of the database schema, specifically focusing on key parts of the system:

- **Users Table:**
  - Stores details about administrators, hosts, and guests, including roles and authentication details.
  - Important columns: user_id, name, email, role (Admin, Host, Guest), and authentication tokens.

- **Properties/Forms Table:**
  - Contains details of each property/host setup, including branding configurations (brand colors, logos, fonts) and customizable fields.
  - Key columns: property_id, host_id (linking to Users), form_configurations, and timestamps.

- **Reservations Table:**
  - Keeps track of booking details and status updates fetched and synchronized with the Guesty API.
  - Key columns: reservation_id, user_id, property_id, status, and custom field mappings.

- **Activity Logs Table:**
  - Logs all significant interactions (like check-in submissions, changes made by administrators) for auditing and analytics.
  - Key columns: log_id, user_id, action, timestamp, and details.

- **Transactions Table:**
  - Handles payment transactions through Stripe, recording upsell services data, commission details, and payment confirmations.
  - Key columns: transaction_id, user_id, amount, payment_status, and related booking reference.

## API Design and Endpoints

The backend communicates with both the frontend and external services through well-designed APIs. Here’s a simple outline:

- **API Approach:**
  - We use RESTful API endpoints that clearly indicate what actions they perform. They are built to be easy to integrate with while providing robust error handling and logging.

- **Key Endpoints Include:**
  - **User Authentication and Management:** Endpoints to sign up, sign in, update user details, and manage roles.
  - **Property and Form Management:** Endpoints for hosts to create and update check-in forms, tailor branding, and build digital guides.
  - **Reservation Sync and Updates:** Endpoints that connect with the Guesty API for real-time data sync, including error logging for field mapping mismatches.
  - **Payment Processing:** Endpoints interacting with Stripe for handling host payments, upsell services, and commission calculations.
  - **Notification Services:** Endpoints that facilitate communication through Twilio for WhatsApp messages, alerting hosts and guests of important updates.

## Hosting Solutions

The backend hosting solution is chosen to provide a balance between cost, scalability, and ease-of-use:

- **Cloud Provider:**
  - **Supabase Hosting:** Our backend is hosted on Supabase cloud services.

- **Benefits of this Approach:**
  - **Reliability:** The cloud environment ensures high uptime and quick recovery in the event of an issue.
  - **Scalability:** Resources are automatically scaled to meet user demand, especially during peak times.
  - **Cost-Effective:** The pay-as-you-go model reduces risks of over-provisioning, ensuring you only pay for what you use.

## Infrastructure Components

Several components work together to deliver a responsive and secure experience:

- **Load Balancers:** Distribute incoming traffic evenly across different backend instances, ensuring no single server gets overwhelmed.
- **Caching Mechanisms:** Help store frequently accessed data temporarily (using, for example, in-memory caches) to speed up response times.
- **Content Delivery Network (CDN):** Delivers static content and media quickly to users worldwide.
- **API Gateways:** Manage and route API requests between the frontend and backend systems, ensuring security and traffic management.

These components work together to ensure that the portal remains fast, reliable, and user-friendly, even during heavy usage periods.

## Security Measures

Securing user data and ensuring authenticity is a top priority. Here’s how it is achieved:

- **Authentication & Authorization:**
  - Using Clerk Auth ensures robust authentication, including multi-role management such as admins, hosts, and guests.
  - Role-based access is enforced so each user only has access to functionalities appropriate for their role.

- **Data Encryption:**
  - Data is encrypted both in transit (using TLS) and at rest in the PostgreSQL database deployed on Supabase.

- **API Security:**
  - All API endpoints are secured with token-based authentication and permission checks.
  - Regular security audits and vulnerability scans help ensure that no outdated or vulnerable components remain.

- **Additional Measures:**
  - Logging: Any errors (e.g., custom field mapping errors) are logged and monitored to avoid security lapses and maintain transparency.
  - Compliance: The system adheres to data protection best practices to safeguard sensitive information.

## Monitoring and Maintenance

To keep the backend running smoothly, several tools and practices are in place:

- **Monitoring Tools:**
  - Built-in tools from Supabase for overseeing database performance and API usage.
  - External monitoring services for tracking load, latency, and uptime.
  - Logging systems to capture errors and unusual activities for prompt investigation.

- **Maintenance Practices:**
  - Regular updates and patches are applied to the backend components (both Supabase functions and external API integrations).
  - Scheduled backups of the database ensure data is not lost and that recovery can be performed if needed.

## Conclusion and Overall Backend Summary

In summary, the backend for the GoRently Portal project is designed with a focus on reliability, scalability, and security. Here’s a recap:

- It uses a modular and easy-to-maintain architecture built around Supabase (with PostgreSQL) and Clerk Auth for seamless user management and security.
- The database schema is designed to clearly separate user data, property configurations, reservations, and billing details, making it easy to manage and extend.
- RESTful APIs ensure that the frontend, real-time third-party integrations such as Guesty, Stripe, and Twilio, communicate reliably and efficiently with the backend.
- Hosting on cloud solutions like Supabase provides high availability, automatic scaling, and cost-effective performance.
- Comprehensive security measures, combined with regular monitoring and maintenance, maintain data integrity and protect against unauthorized access.

This structured and clearly defined backend setup is key to delivering a robust customer experience platform that caters effectively to administrators, hosts, and guests alike.