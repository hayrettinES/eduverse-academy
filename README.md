<div align="center">

# 🎓 EduVerse Academy

**An online course platform where donors can sponsor learning.**
Instructors publish courses, students learn, donors fund, and an AI assistant helps along the way.

![.NET](https://img.shields.io/badge/.NET-10-0c0702?style=for-the-badge&logo=dotnet&logoColor=ffb000)
![ASP.NET Core MVC](https://img.shields.io/badge/ASP.NET_Core-MVC-0c0702?style=for-the-badge&logoColor=ffb000)
![SQLite](https://img.shields.io/badge/SQLite-local_db-0c0702?style=for-the-badge&logo=sqlite&logoColor=ffb000)
![AI](https://img.shields.io/badge/AI-assistant-ffb000?style=for-the-badge&logoColor=0c0702)

</div>

```text
~$ ./eduverse-academy --roles
  student      browse · cart · buy with balance or from the donation pool · track progress
  instructor   create courses · upload lessons & documents · answer reviews
  donor        fill the donation pool so students who can't pay still get in
  admin        approve donations · publish courses · manage users and categories
```

## ✨ Features
- **4 roles, 4 panels:** student, instructor, donor, admin. Each has its own dashboard.
- **Accounts:** e-mail sign-up with a verification link, hashed passwords, cookie sessions. Google sign-in is optional.
- **Profile completion:** after first login, students and instructors are asked for missing details (goals, expertise, …).
- **Courses:** categories, sections, video + PDF per lesson, progress tracking, reviews, replies and lesson comments.
- **Cart, balance and purchases:** students top up a balance, fill a cart and buy courses.
- **Donation pool:** donors (and students) donate; once an admin approves, the money goes into a pool that students can use to get courses for free.
- **AI assistant:** a chat widget on every page, with saved conversations. It works with OpenRouter, OpenAI or Gemini, and rotates over a pool of API keys.

## 🧱 Architecture
```text
Controllers/   Admin · Assistant · Bagisci (donor) · Egitmen (instructor) · Hesap (account)
               Home · Ogrenci (student) · Profil · Sepet (cart)
Servisler/     PlatformServisi        all business rules
               SqliteKomutServisi     raw SQL over the sqlite3 CLI
               VeritabaniHazirlayici  creates tables + demo data on first run
               *AssistantServisi      OpenRouter / OpenAI / Gemini clients
               SmtpEpostaServisi      verification mails
Views/         Razor views per role, shared layout + AI widget
```
The database (`Veriler/eduverse.db`) and its 14 tables are created automatically the first time the app starts.

## 🚀 Run it
1. Install the **.NET 10 SDK**.
2. Download `sqlite3.exe` from [sqlite.org/download](https://www.sqlite.org/download.html) ("sqlite-tools" for Windows) and put it next to `EduVerseAcademy.csproj`.
3. Add your own keys with user-secrets. They stay on your PC and never go into git:
   ```bash
   dotnet user-secrets set "SmtpAyarlari:KullaniciAdi" "you@gmail.com"
   dotnet user-secrets set "SmtpAyarlari:Sifre" "<gmail app password>"
   dotnet user-secrets set "SmtpAyarlari:Gonderen" "you@gmail.com"
   dotnet user-secrets set "AI:OpenRouter:ApiKey" "<openrouter key>"
   # optional Google sign-in
   dotnet user-secrets set "Authentication:Google:ClientId" "<client id>"
   dotnet user-secrets set "Authentication:Google:ClientSecret" "<client secret>"
   ```
4. Start it:
   ```bash
   dotnet run
   ```
   Then open http://localhost:5003.

All keys are optional: without SMTP no mails are sent, without an AI key the assistant is off, without Google credentials the Google button is hidden.

### Demo accounts (created on first run)
| role | e-mail | password |
|---|---|---|
| admin | `admin@eduverse.local` | `Admin123!` |
| instructor | `egitmen@eduverse.local` | `Egitmen123!` |
| student | `ogrenci@eduverse.local` | `Ogrenci123!` |

> Change these before you deploy anywhere public.

## 👥 Team
Built as a team project with [Muhammedduman06](https://github.com/Muhammedduman06).

<div align="center"><sub>part of <a href="https://github.com/hayrettinES">hayrettinOS</a> · <code>~$ ./explore --everything --slowly</code></sub></div>
