# 🔒 Monorepo: SSO and Secured Resource Applications

This repository hosts a solution demonstrating Single Sign-On (SSO) authentication using JWT cookies across multiple Next.js frontend applications, secured by a C#/.NET backend API.

The project utilizes `localtest.me` for shared cookie domains (`.localtest.me`) to facilitate seamless authentication and authorization between the frontend services.

---

## 🌿 Branching Structure

Each component of the project lives on its dedicated branch. The `main` branch serves only as a documentation hub.

| Component | Technology | Branch | Description |
| :--- | :--- | :--- | :--- |
| **SSO Auth Backend** | C# / .NET Web API | [`auth-backend`](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME/tree/sso-auth-backend) | Handles user registration, login, JWT issuance, and OTP/2FA verification. |
| **SSO Auth Frontend** | Next.js (Client/Server) | [`auth-frontend`](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME/tree/sso-auth-frontend) | The main login portal. Supports English and Amharic localization. |
| **Movies Frontend** | Next.js (Client/Server) | [`app1-frontend`](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME/tree/movies-frontend) | The secured resource application (Movies CRUD). Authenticates via the shared SSO cookie. |

*(**NOTE:** Remember to update the links above with your actual GitHub repository details.)*

---

## 🚀 Getting Started

### Prerequisites

* [.NET SDK](https://dotnet.microsoft.com/download) (Version 8.0 or newer recommended)
* [Node.js](https://nodejs.org/) (Version 18 or newer)
* [Yarn](https://classic.yarnpkg.com/en/docs/install) or [npm](https://www.npmjs.com/)

### 1. Backend Setup (`sso-auth-backend` branch)

1.  Clone the branch: `git clone -b sso-auth-backend YOUR_REPO_URL`
2.  Navigate to the directory: `cd sso-auth-backend`
3.  Restore dependencies: `dotnet restore`
4.  Run the application (requires database setup): `dotnet run`

### 2. Frontend Setup (Auth & Movies)

1.  Clone the frontend branches:
    * `git clone -b sso-auth-frontend YOUR_REPO_URL sso-auth-frontend`
    * `git clone -b movies-frontend YOUR_REPO_URL movies-frontend`
2.  Install dependencies in each directory: `npm install` (or `yarn install`)
3.  Run the development servers: `npm run dev` in each directory.

---

## 🌐 Localization (i18n)

Both frontend applications support **Amharic (`am`)** and **English (`en`)** using query parameters.

To switch the language, append `?lang=am` or `?lang=en` to the URL. If no parameter is provided, the application defaults to English.

**Example:**
* English Login: `http://authapp.localtest.me:3000/login`
* Amharic Login: `http://authapp.localtest.me:3000/login?lang=am`

---

## 🔑 Authentication Flow Summary

1.  User accesses `movies-frontend` (http://app1.localtest.me:3001).
2.  `movies-frontend` tries to fetch data from the C# API (`api.app1.localtest.me`).
3.  If the shared **SSO JWT Cookie** is missing, the API returns **401 Unauthorized**.
4.  The frontend redirects the user to the **Login Portal** (`sso-auth-frontend`), passing the `returnUrl`.
5.  Upon successful login, the C# API sets the shared cookie for `.localtest.me`.
6.  The user is redirected back to `movies-frontend`, which now successfully authenticates the API request using the new cookie.

# 🔒 Monorepo: Six-Component SSO and Secured Applications

This repository hosts a solution demonstrating a comprehensive **Single Sign-On (SSO)** architecture. It includes dedicated C#/.NET Web API backends and Next.js frontends for a central authentication portal (`auth-*`) and two distinct secured applications (`app1-*` and `app2-*`).

The entire system relies on **shared JWT cookies** across the `.localtest.me` domain to facilitate seamless, secure authentication and authorization between all components.

---

## 🌿 Branching Structure

Each component of the project lives on its dedicated, isolated branch. The `main` branch is reserved solely for repository documentation and configuration files.

| Component | Technology | Branch | Description |
| :--- | :--- | :--- | :--- |
| **SSO Auth API** | C# / .NET | [`auth-backend`](#set-up-the-c-backend-services) | Handles user registration, login, JWT issuance, and OTP/2FA verification. |
| **SSO Auth Portal** | Next.js | [`auth-frontend`](#set-up-the-nextjs-frontend-applications) | The main login and dashboard portal. Supports **English/Amharic localization**. |
| **App 1 API (Movies)**| C# / .NET | [`app1-backend`](#set-up-the-c-backend-services) | Secured API for App 1 (e.g., Movies CRUD). Validates SSO JWT. |
| **App 1 Frontend**| Next.js | [`app1-frontend`](#set-up-the-nextjs-frontend-applications) | Secured resource application 1 (e.g., Movies App). |
| **App 2 API (Other)** | C# / .NET | [`app2-backend`](#set-up-the-c-backend-services) | Secured API for App 2 (e.g., Course Resources). Validates SSO JWT. |
| **App 2 Frontend**| Next.js | [`app2-frontend`](#set-up-the-nextjs-frontend-applications) | Secured resource application 2 (e.g., Other App). |

---

## 🛠️ Step-by-Step Setup Guide

Follow these steps to clone the repository and run all six applications on your local machine.

### Prerequisites

* **[.NET SDK](https://dotnet.microsoft.com/download)** (Version 8.0 or newer recommended)
* **[Node.js](https://nodejs.org/)** (Version 18 or newer)
* **Git** installed and configured.

### Step 1: Clone and Prepare Local Folders

Because the projects are split across different branches, you must clone the repository multiple times, each time checking out a different branch into its corresponding local folder.

```bash
# 1. Set the URL of your GitHub repository
REPO_URL="YOUR_GITHUB_REPO_URL_HERE" 

# 2. Clone the projects into their respective local directories:
git clone -b auth-frontend $REPO_URL auth-frontend
git clone -b auth-backend $REPO_URL auth-backend
git clone -b app1-frontend $REPO_URL app1-frontend
git clone -b app1-backend $REPO_URL app1-backend
git clone -b app2-frontend $REPO_URL app2-frontend
git clone -b app2-backend $REPO_URL app2-backend
