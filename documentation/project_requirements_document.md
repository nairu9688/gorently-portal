# Project Requirements Document (PRD) – GoRently Portal

## 1. Project Overview

GoRently Portal is an online customer experience platform designed especially for short-term rental hosts. It empowers hosts to manage guest interactions seamlessly through a modern, intuitive web application. The platform centralizes various functions such as online check-in, upsell service sales, and digital guide experiences for guests, while integrating exclusively with the Guesty API—the central property management system. By offering distinct interfaces for administrators, hosts, and guests, the portal bridges the gap between operational management and effective customer communication.

This project is being built to simplify and modernize the short-term rental process for all stakeholders. The key objectives include enhancing guest experiences through smooth digital interactions, streamlining the check-in process, and generating revenue through upsell services. Success will be measured by the improved efficiency of property management workflows, real-time synchronization with Guesty, increased upsell service adoption, and high user satisfaction ratings across both host and guest interfaces.

## 2. In-Scope vs. Out-of-Scope

**In-Scope:**

*   Complete development of an online portal with three interfaces: Administrator, Host, and Guest.
*   Administrator dashboard with subscriber management, activity logs, and comprehensive analytics.
*   Host portal with a flexible online check-in form builder supporting various field types (e.g., text, multiple choice, file uploads) with advanced validations, mandatory/optional options, and conditional logic.
*   Customization features for hosts including brand personalization (color palettes, logo uploads, fonts).
*   Digital Guide Builder that supports rich content (images, text, links, emojis, titles) and the generation of property pages with QR codes.
*   Upsell Services Module covering fixed, request-based, and custom upsell requests, including adjustable pricing workflows.
*   Integration with external systems such as Guesty API for real-time data synchronization (reservations, custom field updates) and Stripe for handling payments (with a 2% commission on transactions).
*   WhatsApp notifications via Twilio and email alerts.
*   Advanced multi-role user management for hosts (allowing roles like property manager or concierge).
*   Responsive, mobile-friendly interface design.
*   Logging mechanism for mismatches or errors during Guesty custom field updates.

**Out-of-Scope:**

*   Any PMS integration other than Guesty.
*   Complex compliance or legislative requirements (like GDPR) beyond secured handling via Supabase.
*   Overly customized analytics for roles outside administrators and hosts (e.g., separate, detailed reports for concierges).
*   In-depth onboarding tutorials or guided walkthroughs beyond a basic help section.
*   Offline capabilities or app versions beyond the responsive web application.

## 3. User Flow

A new user begins their journey by accessing the respective interface based on their role. An administrator logs in to a centralized dashboard where they immediately see an overview of all subscribers, view detailed activity logs, and review real-time analytics. The administrator can drill down into each subscriber’s usage, monitor reservation activities, and track overall platform health. This flow ensures that they can manage and support the entire platform with clarity and efficiency.

Hosts log into a dedicated portal after successfully authenticating and linking their Guesty and Stripe accounts. Once inside, they can easily choose and configure a personalized design through brand settings and then build custom check-in forms using a wide selection of field types and advanced validations. Hosts can further personalize the guest experience by constructing digital guides and setting up upsell services, with real-time notifications via Twilio and email keeping them updated. Meanwhile, guests receive an individual link that leads them to a simple, guided check-in process and a rich digital guide page with clear upsell options, ensuring a seamless transition from booking to check-in.

## 4. Core Features

*   **Administrator Dashboard:**

    *   Centralized view of all subscribers and their activity logs.
    *   Real-time performance analytics and reporting.
    *   Detailed tracking of guest check-ins and upsell transactions.

*   **Host Portal:**

    *   **Online Check-In Form Builder:** Drag-and-drop interface supporting multiple field types (single choice, multiple choice, text, numerical inputs, file uploads) with advanced validations (e.g., regex, conditional logic).

    *   **Customization Settings:** Options to select color palettes, upload logos, and choose fonts (Plus Jakarta Sans, Montserrat).

    *   **Digital Guide Builder:** Allows hosts to create interactive guides with rich content (text, images, links, emojis, and titles) and generate public property pages with QR code support.

    *   **Upsell Services Management:** Three upsell categories:

        *   Fixed Upsells for immediate purchase.
        *   Request-Based Upsells where guest requests trigger host notifications.
        *   Custom Upsell Requests with host-controlled pricing adjustments.

    *   **Account Integrations:** Seamless linking with Guesty (via API token) and Stripe (via Stripe Connect-like integration) for processing payments and updating custom fields.

    *   **Real-Time Notifications:** Alerts (via email and Twilio-powered WhatsApp) to inform hosts of check-in events, upsell requests, and any mismatches/errors.

*   **Guest Interface:**

    *   **Online Pre-Check-In:** Step-by-step guided form matching host’s configuration.
    *   **Digital Guide & Upsell Services:** Interactive display of property notes, upsell service options, and custom guide content.
    *   **Public Property Page:** Accessible via QR code for in-apartment use, ensuring easy access to critical property information.

*   **User Management:**

    *   Support for complex role delegation within host teams (e.g., property manager, concierge).
    *   Controlled access levels based on designated roles.

## 5. Tech Stack & Tools

*   **Frontend:**

    *   Next.js for the application framework.
    *   Tailwind CSS for responsive and modern styling.
    *   Typescript to ensure robust and error-free code.
    *   Shadcn UI for pre-built, customizable UI components.

*   **Backend:**

    *   Supabase for back-end services and database management; ensures security and scalability.
    *   Clerk Auth for user authentication.
    *   Guesty API for real-time PMS integration.
    *   Stripe for payment processing (including Stripe Connect-like integration for account linking and commission handling).

*   **Additional Integrations:**

    *   Twilio for WhatsApp messaging to deliver real-time notifications.
    *   Open AI for any potential enhancements in user interactions or automated functionalities.

*   **IDE & Plugin Integrations:**

    *   Lovable.dev for generating front-end and full-stack web apps.
    *   Cursor as an advanced IDE offering real-time suggestions to streamline development.

## 6. Non-Functional Requirements

*   **Performance:**

    *   Real-time synchronization with Guesty API for all reservation data and custom field updates.
    *   Ensure minimal load times and responsive interactions across the platform.

*   **Security:**

    *   Data protection through Supabase’s secure back-end services.
    *   Secure authentication using Clerk Auth and encrypted communications.
    *   Error logging for mismatches and failures in data transfers between Guesty and the portal.

*   **Usability:**

    *   A modern, minimalist design that is intuitive for administrators, hosts, and guests.
    *   Fully responsive and mobile-friendly design ensuring consistent usage across desktops, tablets, and mobile devices.
    *   Clear notification system for real-time updates via email and WhatsApp.

*   **Reliability:**

    *   High availability and fault tolerance expected from integrating real-time systems (Guesty, Stripe, Twilio).
    *   System should handle high concurrency, particularly during peak check-in times.

## 7. Constraints & Assumptions

*   It is assumed that the Guesty API will be available and reliable for real-time data synchronization.
*   Stripe integration must support direct host account linking with a 2% commission automatically applied to all transactions.
*   The platform will rely on Twilio for WhatsApp notifications, so any limits or rate restrictions imposed by Twilio need to be taken into consideration.
*   Supabase is assumed to provide secure, scalable back-end services without specific compliance mandates beyond standard data security.
*   Branding assumptions include the use of specified colors (#2383f4, #2d323e, #1e232d, #f1f1f1) and the fonts Plus Jakarta Sans and Montserrat.
*   It is assumed that the platform is purely web-based and does not require native mobile app development at this stage.
*   The advanced check-in form builder must support comprehensive custom field validations including regex and conditional logic.

## 8. Known Issues & Potential Pitfalls

*   **API Rate Limits:**

    *   Guesty and Stripe APIs might impose rate limits. It is crucial to implement request throttling and robust error handling to ensure data consistency and prevent data loss.

*   **Real-Time Synchronization:**

    *   Real-time updates can be challenging due to network latency or API downtime. Implement fallback and retry mechanisms for resilient data synchronization.

*   **Custom Field Mapping Errors:**

    *   Mismatches between host-defined custom field IDs and Guesty fields may occur. A detailed logging and notification system should capture these mismatches, allowing hosts to review and adjust mappings.

*   **Complex User Management:**

    *   Delegating various roles (e.g., property manager, concierge) introduces complexity. Ensure that permission levels are clearly defined and tested rigorously to avoid unauthorized access or data breaches.

*   **Notification Overload:**

    *   With real-time notifications sent to hosts via email and WhatsApp, there is a risk of overwhelming the user with alerts. Define clear notification thresholds and preferences to mitigate this risk.

*   **Responsive Design:**

    *   Ensuring a seamless experience across multiple devices may lead to unexpected UI issues. Extensive testing across various screen sizes and platforms is essential to ensure UI consistency and usability.

This PRD outlines every necessary detail intended for the AI model to generate subsequent technical documents without ambiguity. Each section has been expressly detailed in everyday language, ensuring clarity for a smooth development process.
