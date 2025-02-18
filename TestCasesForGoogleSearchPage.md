# Test Cases for Google Search Page

## **1️⃣ Functional Test Cases**
| **Test Case ID** | **Test Scenario** | **Steps to Execute** | **Expected Result** |
|------------------|------------------|----------------------|---------------------|
| TC-001 | Verify that the Google homepage loads successfully | 1. Open `https://www.google.com/` <br> 2. Observe the UI elements | Google logo, search box, and search buttons should be displayed |
| TC-002 | Verify that the user can enter text into the search bar | 1. Open Google homepage <br> 2. Type "Selenium WebDriver" in the search box | Text should be entered successfully |
| TC-003 | Verify that clicking the "Google Search" button displays search results | 1. Type "Selenium WebDriver" <br> 2. Click "Google Search" | Search results page should be displayed |
| TC-004 | Verify that pressing "Enter" key submits the search | 1. Type "Selenium WebDriver" <br> 2. Press `Enter` | Search results page should be displayed |
| TC-005 | Verify that clicking "I'm Feeling Lucky" redirects to the first result | 1. Type "Selenium WebDriver" <br> 2. Click "I'm Feeling Lucky" | User should be redirected to the top search result directly |

---

## **2️⃣ UI & UX Test Cases**
| **Test Case ID** | **Test Scenario** | **Steps to Execute** | **Expected Result** |
|------------------|------------------|----------------------|---------------------|
| TC-006 | Verify that the Google logo is displayed correctly | 1. Open Google homepage <br> 2. Check the Google logo | The Google logo should be visible and correctly displayed |
| TC-007 | Verify that the search box is centered and properly aligned | 1. Open Google homepage <br> 2. Check alignment | The search bar should be centered |
| TC-008 | Verify that search suggestions appear when typing in the search bar | 1. Type "Selenium" in the search box | A dropdown with suggestions should appear |
| TC-009 | Verify that clicking on a search suggestion auto-fills the search bar | 1. Type "Selenium" <br> 2. Click a suggestion | The search bar should be auto-filled with the clicked suggestion |

---

## **3️⃣ Negative Test Cases**
| **Test Case ID** | **Test Scenario** | **Steps to Execute** | **Expected Result** |
|------------------|------------------|----------------------|---------------------|
| TC-010 | Verify searching with an empty input field | 1. Click "Google Search" without entering anything | Page should not navigate anywhere |
| TC-011 | Verify special characters input | 1. Type `@#$%^&*` in the search box <br> 2. Press Enter | Google should return relevant results or a message |
| TC-012 | Verify long text input handling | 1. Type a string of 500+ characters <br> 2. Press Enter | Google should return relevant results without crashing |

---

## **4️⃣ Compatibility Test Cases**
| **Test Case ID** | **Test Scenario** | **Steps to Execute** | **Expected Result** |
|------------------|------------------|----------------------|---------------------|
| TC-013 | Verify Google Search works in different browsers | 1. Open Google in Chrome, Firefox, Edge, Safari <br> 2. Perform a search | The search should work consistently across browsers |
| TC-014 | Verify Google Search works on mobile devices | 1. Open Google on an iOS & Android device <br> 2. Perform a search | The search should work correctly on mobile browsers |

---

## **5️⃣ Performance & Security Test Cases**
| **Test Case ID** | **Test Scenario** | **Steps to Execute** | **Expected Result** |
|------------------|------------------|----------------------|---------------------|
| TC-015 | Verify page load time | 1. Open Google homepage <br> 2. Measure page load time | Page should load in **less than 3 seconds** |
| TC-016 | Verify search results load time | 1. Perform a search query <br> 2. Measure response time | Results should load in **less than 2 seconds** |
| TC-017 | Verify that HTTPS is enforced | 1. Try opening `http://www.google.com/` | The page should redirect to **HTTPS automatically** |

---

## **6️⃣ Accessibility Test Cases**
| **Test Case ID** | **Test Scenario** | **Steps to Execute** | **Expected Result** |
|------------------|------------------|----------------------|---------------------|
| TC-018 | Verify screen reader compatibility | 1. Use NVDA or JAWS screen reader <br> 2. Navigate through the page | The screen reader should correctly announce elements |
| TC-019 | Verify keyboard accessibility | 1. Navigate Google using only the keyboard <br> 2. Press `Tab` and `Enter` | The search bar and buttons should be accessible via keyboard |
| TC-020 | Verify contrast ratio for visibility | 1. Use a contrast checker tool <br> 2. Validate the contrast of text and background | Google should meet **WCAG 2.1 contrast standards** |

---

## **7️⃣ Automation Feasibility**
The following test cases are **highly suitable** for **Selenium automation**:

- **Functional Tests** (TC-002 to TC-005)
- **UI Tests** (TC-008, TC-009)
- **Negative Tests** (TC-010 to TC-012)
- **Performance Tests** (TC-015, TC-016)

---

Would you like a **Selenium script** for automating some of these test cases? 🚀😊
