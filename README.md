/
├─ README.md
├─ SECURITY.md
├─ LICENSE
└─ matrix_email_sender.py
# 👑 GrandMasterAngel

**RITTHIKRAI KIRIKAN**  
Founder & CEO | Technology Leader  
GitHub: https://github.com/GrandMasterAngel

---

## 🧠 About the Founder

I am a **Founder & CEO** with a strong background in  
**production-grade software development and system architecture**.

I focus on building technology that:
- Works in real-world business environments
- Is secure and reliable by design
- Can scale sustainably over the long term

Expertise areas:
- 🤖 AI
- 🌐 Web3 & Blockchain
- ⚙️ Backend & Infrastructure
- 🔐 Security & Reliability

I don’t just build systems that “work” —  
I build systems that are **stable, scalable, and valuable in the real world**.

---

## 🎯 Purpose of This Repository

- 📘 Technical knowledge base & references
- 🧭 Production-level system design principles
- 🚀 Foundation for real platforms and products

**Production-first · Security-first · Long-term thinking**

---

## 🧭 Vision

To build technology that is **practical, secure, and scalable**,  
serving as long-term infrastructure for businesses and people to grow.

---

## 🎯 Mission

- Build production-grade systems
- Design for long-term scalability
- Treat security as a first-class concern
- Apply AI and Web3 with real purpose
- Establish standards that help teams grow together

---

## 🧠 Core Philosophy

- Technology solves real problems
- Security is not optional
- Scalability is designed, not added
- Long-term value beats short-term hype

---

## ⚙️ Technology Stack

### Backend
- Python (FastAPI)
- REST / Async APIs

### AI & Data
- LLM APIs
- Vector Databases
- Data Pipelines

### Web3
- EVM-compatible chains
- RPC Providers
- Smart Contract Integration

### Infrastructure
- Docker
- Environment-based configuration
- CI/CD ready

### Security
- Secret Management
- JWT / RBAC

---

## 🏗️ System Architecture (High-Level)

**Client → API → Services → Core → Data**

- Client: Web / Mobile
- API: FastAPI, Authentication, Rate limiting
- Services: Business logic / AI / Web3
- Core: Configuration, Security
- Data: Databases, Cache, External APIs

---

## 🔁 Architecture Principles

- Separation of concerns
- Stateless services
- Config-driven environments
- Scale-ready infrastructure

---

## 🛣️ Technical Roadmap

- **Phase 1:** Foundation
- **Phase 2:** Platform (AI / Web3)
- **Phase 3:** Scale & Observability

---

## 📜 License

- **CC BY 4.0** — Documentation
- **MIT** — Source Code
# 🔐 Security Policy

## 🛡️ Supported Versions

This project follows a **latest-version-only** support policy.

| Version / Branch | Supported |
|------------------|-----------|
| `main`           | ✅ Yes     |
| Older versions   | ❌ No      |

Security patches are released **only** for the latest stable version.

---

## 🚨 Reporting a Vulnerability

If you discover a security vulnerability, please report it responsibly.

📧 **Contact:**  
gingzaindy9999@gmail.com

### Please include:
- Description of the issue
- Steps to reproduce (if applicable)
- Potential impact
- Proof-of-concept (if safe to share)

⚠️ **Do NOT** disclose vulnerabilities publicly before coordination.

---

## ⏱️ Response Timeline

- Initial response: within **48–72 hours**
- Assessment & validation: ASAP
- Fix or mitigation: based on severity

Critical issues are prioritized.

---

## 🔍 Scope

This policy applies to:
- Email delivery logic and SMTP usage
- Credential and secret handling
- CLI input and argument parsing
- Environment configuration
- External service integrations

---

## 🔐 Security Principles

- Security is not optional
- Secrets must never be hard-coded
- Least privilege by default
- Fail safely, not silently
- Production-first mindset

---

## 🤝 Responsible Disclosure

We value responsible disclosure and may acknowledge valid reports in:
- Release notes
- Documentation
- Security advisories

---

## 📜 Legal Notice

By reporting vulnerabilities, you agree to:
- Act in good faith
- Avoid service disruption
- Respect user privacy and applicable laws

---

**Thank you for helping keep this project secure.**  
— *GrandMasterAngel (RITTHIKRAI KIRIKAN)* 👑
"""
Matrix Email Sender
Author: GrandMasterAngel (RITTHIKRAI KIRIKAN)
Contact: gingzaindy9999@gmail.com

Command-line tool for sending notification emails
(e.g. Crypto / Matrix alerts).
"""

import smtplib
import argparse
import datetime
import sys
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart


def send_matrix_email(
    to_email: str,
    subject: str,
    body: str,
    from_email: str,
    smtp_server: str,
    smtp_port: int,
    smtp_username: str,
    smtp_password: str,
):
    """Send a notification email via SMTP."""
    msg = MIMEMultipart()
    msg["From"] = from_email
    msg["To"] = to_email
    msg["Subject"] = subject

    msg.attach(MIMEText(body, "plain"))

    try:
        with smtplib.SMTP(smtp_server, smtp_port) as server:
            server.starttls()
            server.login(smtp_username, smtp_password)
            server.send_message(msg)
    except Exception as exc:
        print(f"[ERROR] Failed to send email: {exc}")
        sys.exit(1)


def main():
    parser = argparse.ArgumentParser(description="Matrix Email Sender")
    parser.add_argument("--to", required=True, help="Recipient email")
    parser.add_argument("--subject", required=True, help="Email subject")
    parser.add_argument("--body", required=True, help="Email body")
    parser.add_argument("--from-email", required=True, help="Sender email")
    parser.add_argument("--smtp-server", required=True, help="SMTP server")
    parser.add_argument("--smtp-port", type=int, default=587)
    parser.add_argument("--smtp-username", required=True)
    parser.add_argument("--smtp-password", required=True)

    args = parser.parse_args()

    send_matrix_email(
        to_email=args.to,
        subject=args.subject,
        body=args.body,
        from_email=args.from_email,
        smtp_server=args.smtp_server,
        smtp_port=args.smtp_port,
        smtp_username=args.smtp_username,
        smtp_password=args.smtp_password,
    )


if __name__ == "__main__":
    main()
/
├─ matrix_email_sender/
│  ├─ __init__.py
│  ├─ cli.py
│  ├─ emailer.py
│  └─ config.py
├─ .env.example
├─ .gitignore
├─ README.md
├─ SECURITY.md
├─ pyproject.toml
└─ LICENSE
# SMTP Configuration
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your_email@gmail.com
SMTP_PASSWORD=your_app_password

.env
__pycache__/
*.pyc
.venv/
import os
from dotenv import load_dotenv

load_dotenv()

SMTP_SERVER = os.getenv("SMTP_SERVER")
SMTP_PORT = int(os.getenv("SMTP_PORT", "587"))
SMTP_USERNAME = os.getenv("SMTP_USERNAME")
SMTP_PASSWORD = os.getenv("SMTP_PASSWORD")
FROM_EMAIL = os.getenv("FROM_EMAIL")

def validate_config():
    missing = [
        k for k, v in {
            "SMTP_SERVER": SMTP_SERVER,
            "SMTP_USERNAME": SMTP_USERNAME,
            "SMTP_PASSWORD": SMTP_PASSWORD,
            "FROM_EMAIL": FROM_EMAIL,
        }.items() if not v
    ]
    if missing:
        raise RuntimeError(f"Missing environment variables: {', '.join(missing)}")
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

def send_email(
    to_email: str,
    subject: str,
    body: str,
    from_email: str,
    smtp_server: str,
    smtp_port: int,
    smtp_username: str,
    smtp_password: str,
):
    msg = MIMEMultipart()
    msg["From"] = from_email
    msg["To"] = to_email
    msg["Subject"] = subject
    msg.attach(MIMEText(body, "plain"))

    with smtplib.SMTP(smtp_server, smtp_port) as server:
        server.starttls()
        server.login(smtp_username, smtp_password)
        server.send_message(msg)
import argparse
from matrix_email_sender.config import (
    SMTP_SERVER, SMTP_PORT, SMTP_USERNAME,
    SMTP_PASSWORD, FROM_EMAIL, validate_config
)
from matrix_email_sender.emailer import send_email

def main():
    validate_config()

    parser = argparse.ArgumentParser(description="Matrix Email Sender CLI")
    parser.add_argument("--to", required=True)
    parser.add_argument("--subject", required=True)
    parser.add_argument("--body", required=True)

    args = parser.parse_args()

    send_email(
        to_email=args.to,
        subject=args.subject,
        body=args.body,
        from_email=FROM_EMAIL,
        smtp_server=SMTP_SERVER,
        smtp_port=SMTP_PORT,
        smtp_username=SMTP_USERNAME,
        smtp_password=SMTP_PASSWORD,
    )
matrix-email \
  --to user@example.com \
  --subject "Matrix Alert" \
  --body "BTC crossed threshold"