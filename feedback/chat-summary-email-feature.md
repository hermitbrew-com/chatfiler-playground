# Feature Request: Email Chat Summary

## Category
Feature / Integrations

## Overview
Add the ability to send a generated **chat summary** directly to an email address.

## Problem
Currently, chat summaries are only available within the ChatFiler interface or as files stored in the repository. Users who want to:
- Share summaries with teammates
- Save summaries to their inbox
- Forward summaries to external systems (ticketing, CRM, notes)

must manually copy or download the content.

## Proposed Feature
Introduce a **"Send Summary via Email"** option that allows users to:
- Enter one or more email addresses
- Choose the summary format (plain text or Markdown)
- Optionally include metadata (date, session folder, conversation title)

## Example Workflow
1. User clicks **Generate Chat Summary**
2. User selects **Send via Email**
3. Modal appears:
   - Email address field(s)
   - Subject line (auto-filled, editable)
   - Format toggle (Text / Markdown)
4. User clicks **Send**

## Optional Enhancements
- Save frequently used email addresses
- Auto-send summaries at end of session
- Email delivery confirmation
- Webhook alternative for automation tools

## Why This Matters
- Reduces friction for sharing and archiving conversations
- Improves collaboration and documentation workflows
- Makes ChatFiler more useful for teams and professionals

## Priority
Medium–High

## Notes
This feature would pair well with session folders and public/private sharing controls in the future.
