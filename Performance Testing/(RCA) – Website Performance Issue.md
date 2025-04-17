# 📝 Root Cause Analysis (RCA) – Website Performance Issue

## 📅 Date:
April 16, 2025

## 👤 Reported By:
QA Team

## 🧠 Issue Summary:
Users reported that the **Checkout Page** on the e-commerce website was taking **12–15 seconds** to load during peak usage.

---

## 🔁 Steps to Reproduce:
1. Log in as a regular user.
2. Add 3–5 items to the shopping cart.
3. Proceed to the Checkout page.
4. Measure page load time using browser tools.
5. Observe that the page consistently takes over 12 seconds to load.

---

## 🔬 QA Analysis Steps:

| 🔍 Step | QA Action | Tool Used |
|--------|-----------|-----------|
| **1. Baseline Measurement** | Use Lighthouse or GTmetrix to get page speed score and load breakdown. | Lighthouse / GTmetrix |
| **2. Network Profiling** | Open Chrome Dev Tools > Network tab. Identify slow API requests or large assets. | Browser Dev Tools |
| **3. API Analysis** | Identify which API takes the longest to respond (e.g., `getCartDetails`). Test the same API using Postman to confirm it's slow independently of the UI. | Postman |
| **4. Frontend Bottleneck Check** | Check for large images, unminified JS/CSS files, or blocking scripts in Dev Tools. | Dev Tools > Performance tab |
| **5. Compare Load Across Browsers** | Test in Chrome, Firefox, Edge to see if issue is browser-specific. | Manual Testing |
| **6. Device Responsiveness** | Test on mobile vs. desktop. Check if slow load is due to responsiveness or mobile performance. | Mobile Emulator / Real Devices |
| **7. Session Behavior Testing** | Test with new vs. returning user sessions to rule out caching or stale data issues. | Browser Testing |
| **8. Collaborate with DevOps** | Request backend logs and performance metrics for affected APIs. Validate database call times and server resource usage. | Coordination with DevOps |
| **9. Log and Report** | Capture all observations, screenshots, timings, and attach to the JIRA ticket. | JIRA, Screenshots |

---

## 📊 Observations:

| Tool / Step | Finding |
|-------------|---------|
| Dev Tools (Network) | `getCartDetails` API taking 6–8 seconds |
| Postman | Same API slow with 3+ items in cart |
| Dev Logs | Unoptimized SQL query identified (no index on `UserID`) |
| Image Audit | Banner image on page = 5MB, not compressed |
| Lighthouse | Performance score = 35/100 (very poor) |

---

## 🧩 Root Cause:
- Backend API delay due to **full table scan** from unindexed `UserID` column in SQL.
- Large, uncompressed banner image increasing frontend load time.

---

## 🛠️ Fixes Implemented:
1. Created a **database index** on `Cart.UserID`.
2. Optimized SQL query in `getCartDetails`.
3. Compressed banner image and enabled lazy loading.

---

## ✅ Result After Fix:

| Metric | Before Fix | After Fix |
|--------|------------|-----------|
| Page Load Time | 12–15 seconds | 2.3 seconds |
| API Response Time | ~8 seconds | <500 ms |
| Lighthouse Score | 35 | 91 |

---

## 📌 Recommendations for QA:
- Add **API performance review** to regression checklist.
- Use Lighthouse audits regularly during UI testing.
- Enforce max image size limits during code reviews.
- Include DB indexing awareness in QA–Dev handoff meetings.
- Use **Postman or JMeter** to independently test API latency under various loads.

---

## 👥 Teams Involved:
- QA Team
- Backend Developers
- DevOps Team
- UI/UX Team

