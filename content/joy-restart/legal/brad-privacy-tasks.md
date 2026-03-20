# Brad — Privacy & Data Tasks (Monday)

## Critical (Before April 15)

1. **Fix disclosure links** on ALL four assessments
   - Currently point to "#" (broken)
   - Create a real page using the disclosure text Aaron drafted (see assessment-disclosure.md)
   - Link every assessment's "Disclaimer & Disclosure" to this page

2. **Update consent checkbox text** on ALL four assessments
   - Replace current text with: "I consent to Joy Restart collecting my responses to generate my personalized report. Anonymous, de-identified data may be used to improve our assessments. My individual results are confidential."
   - See consent-checkbox-text.md for full options

3. **Confirm:** Are IP addresses being stored in Formidable Pro?
   - If yes: disable IP storage (Formidable → Global Settings → disable IP tracking)

4. **Confirm:** Is the WP database encrypted at rest? Or plaintext?

5. **Add email-my-results** to Joy, Fear, and Maturity
   - Forgiveness already has this feature
   - This is important: users currently have only one chance to see their report (on screen). If they close the tab, it's gone.

## Important (Before April 15 if time allows)

6. **Implement data retention:** Can Formidable Pro auto-delete entries older than 90 days?
   - If not natively, is there a plugin or cron job approach?
   - Goal: keep only anonymous aggregate data long-term, purge personal entries

7. **Update Privacy Policy** (joyrestart.com/privacy/)
   - Add a section specifically about assessment data
   - What we collect, how we use it, how long we keep it, how to request deletion
   - Aaron can draft the language; Brad implements on the page

## Questions for Brad

- How is Formidable Pro currently storing assessment entries? (wp_frm_items table?)
- Is there any backup/export of assessment data happening?
- Does anyone besides Brad and David have admin access to the WP database?
- Is the site running on managed hosting with automatic security updates?
