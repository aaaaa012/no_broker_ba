# Deployment & Configuration

## ⚙️ Configuration
The application requires the following Environment Variables:

### Backend
| Variable | Description |
| :--- | :--- |
| `PORT` | Application port (e.g., 3000) |
| `JWT_SECRET` | Secret key for signing tokens |
| `DB_HOST` | PostgreSQL Database Host |
| `CORS_ORIGINS` | Allowed frontend domains |

### Frontend
| Variable | Description |
| :--- | :--- |
| `API_BASE_URL` | URL of the backend API |
| `WS_URL` | URL for WebSocket connection |

## 🚀 Deployment Strategy
1.  **Frontend**: Build static assets and serve via CDN (Netlify/Vercel/AWS CloudFront).
2.  **Backend**: Dockerized Node.js container behind Nginx reverse proxy.
3.  **Database**: Managed PostgreSQL (RDS/CloudSQL).
4.  **SSL**: Mandatory for secure data transmission.

## Appendix: Glossary
*   **Listing**: A rental property unit.
*   **Visit**: A physical viewing appointment.
*   **Conversation**: A distinct message thread between two users.
