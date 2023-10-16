---
tags:
  - backend
  - http
source:
  - https://www.youtube.com/watch?v=4HlNv1qpZFY
type:
  - "[[TILT]]"
created: 2023-10-16T19:27:00
areas:
  - "[[API Development]]"
archived: false
---

# Use Cases
- Live Feed
- Showing client progress
- Logging

# Pros
- Lightweight
- HTTP & HTTP/2 compatible
- Firewall friendly (standard)

# Cons
- Proxying is tricky
- L7 L/B challenging (timeouts)
- Stateful, difficult to horizontally scale (could be stateless based on the system architecture)

# When to use
- Alternative for [[Websockets]]
- Long polling functionality