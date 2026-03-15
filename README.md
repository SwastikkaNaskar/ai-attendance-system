# AI-Powered Attendance & Warning System

## Overview
Automated HR workflow built with n8n that processes biometric attendance data, identifies late arrivals, and sends AI-generated warning emails with escalating tone based on strike count.

## Stack
- **Orchestration**: n8n Cloud
- **Storage**: Google Sheets
- **AI**: Groq (Llama 3 — llama3-8b-8192)
- **Email**: Gmail via Google OAuth2
- **Calendar**: Google Calendar via Google OAuth2
- **Trigger**: Webhook (POST)

## How It Works
1. Webhook receives daily Excel file from biometric machine
2. Data is processed — earliest IN = check-in, latest OUT = check-out
3. Late flag set if check-in after 11:00 AM
4. Monthly strike counter updated in Google Sheets
5. Groq AI drafts personalized warning email based on strike level
6. Gmail sends email automatically
7. 3rd strike triggers Google Calendar meeting at 5 PM

## How to Run
1. Import `attendance_workflow.json` into n8n
2. Add credentials: Google OAuth2 (Sheets + Gmail + Calendar), Groq API
3. Set your Google Sheet ID in all Sheets nodes
4. Activate the workflow
5. POST an Excel file to the webhook URL

## Database Schema
### Daily Records
| Employee ID | Name | Date | Check-In | Check-Out | Late Flag |

### Monthly Counter
| Employee ID | Name | Monthly Late Count | Last Warning Date | Month-Year |

## Files
- `attendance_workflow.json` — n8n workflow (ready to import)
- `Attendance_System_Documentation_v2.pdf` — architecture, edge cases, scalability
- `Attendance_Report_Sheet.xlsx` — sample test data
