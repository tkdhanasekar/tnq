YAML (YAML Ain’t Markup Language) is a human-readable data serialization format commonly used for configuration files (e.g., Docker, Kubernetes, CI/CD pipelines).

---

# 1. Basic Structure

YAML is based on **key-value pairs**:

```yaml
name: John
age: 30
```

* `name` and `age` → keys
* `John`, `30` → values

---

# 2. Indentation (Very Important)

YAML uses **spaces (not tabs)** for structure.

```yaml
person:
  name: John
  age: 30
```

* `person` is the parent
* `name` and `age` are nested under it

---

# 3. Data Types

## Strings

```yaml
name: John
city: "Chennai"
```

## Numbers

```yaml
age: 25
price: 99.99
```

## Boolean

```yaml
is_active: true
is_admin: false
```

## Null

```yaml
value: null
```

---

# 4. Lists (Arrays)

### Simple list

```yaml
fruits:
  - apple
  - banana
  - mango
```

### Inline list

```yaml
fruits: [apple, banana, mango]
```

---

# 5. List of Objects

```yaml
employees:
  - name: Alice
    age: 28
  - name: Bob
    age: 32
```

---

# 6. Nested Structures

```yaml
company:
  name: ABC Corp
  location:
    city: Chennai
    country: India
```

---

# 7. Comments

```yaml
# This is a comment
name: John  # Inline comment
```

---

# 8. Multi-line Strings

### Literal (keeps line breaks)

```yaml
description: |
  This is line one
  This is line two
```

### Folded (joins lines)

```yaml
description: >
  This is line one
  This is line two
```

---

# 9. Key Naming Rules

* Use lowercase and hyphens for readability

```yaml
user-name: john_doe
```

---

# 10. Anchors & Aliases (Reuse Values)

```yaml
default: &default_settings
  timeout: 30
  retries: 3

service1:
  <<: *default_settings
  url: http://example.com
```

---

# 11. Environment-style Example

```yaml
app:
  name: myapp
  version: 1.0
  debug: true

database:
  host: localhost
  port: 5432
```

---

# 12. Real-world Example (Docker Compose)

```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "80:80"
```

---

# 13. Real-world Example (Kubernetes Pod)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx
```

---

# 14. Common Mistakes

### 1. Using tabs ❌

```yaml
name: John   # correct uses spaces
```

### 2. Wrong indentation ❌

```yaml
person:
name: John   # wrong
```

### 3. Missing space after colon ❌

```yaml
name:John   # wrong
```

---

# 15. YAML vs JSON

YAML:

```yaml
name: John
age: 30
```

JSON:

```json
{
  "name": "John",
  "age": 30
}
```

YAML is more readable and less verbose.

---

# Summary

YAML basics:

* Uses **indentation (spaces)**
* Supports **key-value pairs**
* Handles **lists, objects, and nesting**
* Widely used in **DevOps tools**

---

## examples:

**50+ YAML practice examples** ranging from beginner to slightly advanced. Try modifying them to strengthen your understanding.

---

# 1–10: Basic Key-Value Practice

```yaml
name: Alice
```

```yaml
age: 25
```

```yaml
city: Chennai
```

```yaml
country: India
```

```yaml
is_student: true
```

```yaml
height: 5.7
```

```yaml
email: alice@example.com
```

```yaml
phone: 9876543210
```

```yaml
status: active
```

```yaml
role: developer
```

---

# 11–20: Multiple Key-Value Pairs

```yaml
name: Bob
age: 30
city: Mumbai
```

```yaml
product: Laptop
price: 75000
available: true
```

```yaml
title: YAML Guide
author: John Doe
pages: 200
```

```yaml
username: admin
password: secret
```

```yaml
brand: Samsung
model: Galaxy S21
```

```yaml
language: Python
version: 3.10
```

```yaml
framework: React
version: 18
```

```yaml
server: nginx
port: 80
```

```yaml
database: mysql
port: 3306
```

```yaml
env: production
debug: false
```

---

# 21–30: Lists

```yaml
fruits:
  - apple
  - banana
  - mango
```

```yaml
numbers:
  - 1
  - 2
  - 3
```

```yaml
colors: [red, green, blue]
```

```yaml
languages:
  - Python
  - Java
  - Go
```

```yaml
cities:
  - Chennai
  - Delhi
  - Bangalore
```

```yaml
tools:
  - Docker
  - Kubernetes
```

```yaml
ports:
  - 80
  - 443
```

```yaml
roles:
  - admin
  - user
```

```yaml
skills:
  - coding
  - testing
```

```yaml
hobbies:
  - reading
  - gaming
```

---

# 31–40: Nested Objects

```yaml
person:
  name: Alice
  age: 25
```

```yaml
address:
  street: 1st Main Road
  city: Chennai
```

```yaml
company:
  name: ABC Corp
  employees: 100
```

```yaml
car:
  brand: Toyota
  model: Camry
```

```yaml
book:
  title: YAML Basics
  author: John
```

```yaml
student:
  name: Ravi
  marks: 85
```

```yaml
course:
  name: DevOps
  duration: 3 months
```

```yaml
server:
  host: localhost
  port: 8080
```

```yaml
app:
  name: MyApp
  version: 1.0
```

```yaml
os:
  name: Linux
  distro: Ubuntu
```

---

# 41–50: List of Objects

```yaml
employees:
  - name: Alice
    age: 25
  - name: Bob
    age: 30
```

```yaml
products:
  - name: Laptop
    price: 50000
  - name: Phone
    price: 20000
```

```yaml
students:
  - name: Ravi
    marks: 80
  - name: Kumar
    marks: 75
```

```yaml
servers:
  - host: 192.168.1.1
    port: 80
  - host: 192.168.1.2
    port: 443
```

```yaml
books:
  - title: Book1
    author: Author1
  - title: Book2
    author: Author2
```

```yaml
cars:
  - brand: Toyota
    model: Corolla
  - brand: Honda
    model: Civic
```

```yaml
orders:
  - id: 1
    amount: 100
  - id: 2
    amount: 200
```

```yaml
users:
  - username: admin
    role: admin
  - username: guest
    role: user
```

```yaml
containers:
  - name: web
    image: nginx
  - name: db
    image: mysql
```

```yaml
apis:
  - name: login
    method: POST
  - name: getUser
    method: GET
```

---

# 51–60: Advanced Practice

```yaml
app:
  name: MyApp
  features:
    - login
    - signup
    - dashboard
```

```yaml
database:
  host: localhost
  ports:
    - 5432
    - 5433
```

```yaml
service:
  name: web
  env:
    NODE_ENV: production
    PORT: 3000
```

```yaml
deployment:
  replicas: 3
  strategy:
    type: RollingUpdate
```

```yaml
config:
  retries: 3
  timeout: 30
  enabled: true
```

```yaml
logging:
  level: info
  format: json
```

```yaml
pipeline:
  stages:
    - build
    - test
    - deploy
```

```yaml
cache:
  enabled: true
  size: 256MB
```

```yaml
auth:
  methods:
    - password
    - oauth
```

```yaml
monitoring:
  enabled: true
  tools:
    - prometheus
    - grafana
```

---

# Bonus: Challenge Exercises

Try writing YAML for:

1. A **Docker Compose file with 2 services**
2. A **Kubernetes Deployment**
3. A **CI/CD pipeline**
4. A **user profile with nested address + hobbies**
5. A **shopping cart with multiple items**
