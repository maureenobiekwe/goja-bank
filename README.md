<h1 align="center">Goja Bank</h1>

<p align="center">
  A fintech banking app used as a system under test for manual and exploratory QA on high-risk money flows.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Appwrite-FD366E?style=flat-square&logo=appwrite&logoColor=white" alt="Appwrite" />
  <img src="https://img.shields.io/badge/Plaid-Sandbox-111111?style=flat-square" alt="Plaid Sandbox" />
  <img src="https://img.shields.io/badge/Dwolla-Sandbox-F26722?style=flat-square" alt="Dwolla Sandbox" />
</p>

---


## The Application

Goja Bank is a personal banking dashboard. Users sign up, link one or more bank accounts through Plaid, view balances and transactions across those accounts, and send money to other users through Dwolla.

| Module               | What it does                                                      |
| -------------------- | ----------------------------------------------------------------- |
| Authentication       | Server-side sign-up and sign-in with form validation              |
| Bank linking         | Connects multiple bank accounts through Plaid Link                |
| Dashboard            | Total balance across linked banks, recent transactions, spending by category |
| My Banks             | Each linked bank with its balance and account details             |
| Transaction history  | Paginated, filterable transactions per bank                       |
| Funds transfer       | Sends money to another user's account through Dwolla              |

## QA Focus Areas

Testing is prioritised by what would hurt a real user or a real business if it broke.

| Area              | Risks under test                                                                 |
| ----------------- | -------------------------------------------------------------------------------- |
| Funds transfer    | Duplicate submission, amount precision and rounding, zero and negative amounts, transfer to self, invalid recipient ID, insufficient funds |
| Balances          | Aggregate total matches the sum of linked accounts; balances refresh after a transfer or a new bank link |
| Bank linking      | Cancelled or failed Plaid flows, linking the same bank twice, expired link tokens |
| Authentication    | Session expiry, access to protected routes after sign-out, validation bypass on sign-up |
| Authorization     | One user viewing or acting on another user's banks or transactions               |
| Transaction history | Pagination boundaries, filter combinations, empty states, ordering by date     |
| Data integrity    | Transaction records in Appwrite match what Plaid and Dwolla return               |
| Responsiveness    | Core flows on mobile, tablet and desktop widths                                  |

## Tech Stack

| Layer         | Technologies                                      |
| ------------- | ------------------------------------------------- |
| Framework     | Next.js, TypeScript                               |
| UI            | Tailwind CSS, shadcn/ui, Chart.js                 |
| Forms         | React Hook Form, Zod                              |
| Backend       | Appwrite (auth and database)                      |
| Integrations  | Plaid (bank linking), Dwolla (transfers)          |

## Running It Locally

### Prerequisites

- [Git](https://git-scm.com/)
- [Node.js](https://nodejs.org/en) and npm
- Free sandbox accounts on [Appwrite](https://appwrite.io/), [Plaid](https://plaid.com/) and [Dwolla](https://www.dwolla.com/)

### 1. Clone and install

```bash
git clone https://github.com/maureenobiekwe/goja-bank.git
cd goja-bank
npm install
```

### 2. Configure environment variables

Create a `.env` file in the project root:

```env
# Next.js
NEXT_PUBLIC_SITE_URL=

# Appwrite
NEXT_PUBLIC_APPWRITE_ENDPOINT=https://cloud.appwrite.io/v1
NEXT_PUBLIC_APPWRITE_PROJECT=
APPWRITE_DATABASE_ID=
APPWRITE_USER_COLLECTION_ID=
APPWRITE_BANK_COLLECTION_ID=
APPWRITE_TRANSACTION_COLLECTION_ID=
APPWRITE_SECRET=

# Plaid
PLAID_CLIENT_ID=
PLAID_SECRET=
PLAID_ENV=sandbox
PLAID_PRODUCTS=
PLAID_COUNTRY_CODES=

# Dwolla
DWOLLA_KEY=
DWOLLA_SECRET=
DWOLLA_BASE_URL=https://api-sandbox.dwolla.com
DWOLLA_ENV=sandbox
```

Keep Plaid and Dwolla on **sandbox**. No real money or real bank data should ever touch this environment.

### 3. Start the app

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

## Test Data

- **Bank linking:** use Plaid's sandbox institutions and its published sandbox login (`user_good` / `pass_good`). Plaid also provides sandbox credentials that trigger specific error states, which are useful for negative testing.
- **Transfers:** run between two test users, each with a linked sandbox bank, so both sides of a transfer can be checked.
- **Users:** create fresh accounts per test session to avoid state carried over from earlier runs.

## Author

**Maureen Obiekwe** — Senior QA Engineer
[GitHub](https://github.com/maureenobiekwe) · [Portfolio](https://maureenobiekwe.com)
# goja-bank
