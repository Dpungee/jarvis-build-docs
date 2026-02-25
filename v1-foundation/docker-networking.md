# Docker Networking — Lessons Learned in V1

## The Problem We Hit
Wanted to run a service inside the Agent Zero container and access it externally. Kept failing.

## Why It Fails
Port bindings are set at container CREATION time. You cannot add new port bindings to an already-running container.

## The Correct Solutions

### Option 1: Modify docker-compose.yml (Cleanest)
```yaml
services:
  agent-zero:
    ports:
      - "50080:80"
      - "8080:8080"  # ← add new port
```
Then: `docker-compose down && docker-compose up -d`
⚠️ This recreates the container — volume data survives, in-container installs don't.

### Option 2: nginx Reverse Proxy (What We Use)
```nginx
location /myapp/ {
    proxy_pass http://localhost:50080/myapp/;
}
```
No container restart needed. This is how Agent Zero itself is accessed externally.

## Current Port Map
| Port | Service | Access |
|------|---------|--------|
| 50080 | Agent Zero dashboard | Via nginx → browser |
| 80/443 | nginx host | External entry point |

## Key Rule
**Never try to expose new ports by running commands inside the container.** It will appear to work but will be unreachable. Always use nginx proxy on the host instead.

