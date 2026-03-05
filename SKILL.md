---
name: app-mapper
description: Map application functionalities, workflows, domains, and features from source code. Use when analyzing a codebase to identify application structure, domains, user workflows, functional areas, and security-relevant features (roles, permissions, authentication, endpoints). Generates three complementary outputs - JSON with full relationship graph, Markdown documentation, and interactive TUI. Language-agnostic detection works with JavaScript, Python, Go, Java, PHP, Ruby, C#, Rust and any language via pattern recognition. Perfect for security assessment preparation (feeding to Hacktron), architecture understanding, feature tracking, and vulnerability surface mapping.
license: MIT
compatibility: Requires source code files or directories. All programming languages supported (language-agnostic). Outputs: JSON (graph-based), Markdown (documentation), TUI (interactive tree view).
metadata:
  author: security-team
  version: "2.0.0"
  category: security, architecture, analysis
  difficulty: beginner
allowed-tools: Read FileSystem Analysis
---

# App Mapper Skill

**PURPOSE**: Analyze source codebases to extract application structure, security-relevant features, workflows, and risk areas.

---

## CRITICAL RULES

**ALWAYS analyze the complete codebase:**
- Read ALL source files provided
- Identify EVERY domain and functional area
- Extract ALL user roles, permissions, and authentication methods
- Map EVERY user-facing workflow
- FLAG ALL security-sensitive components

**NEVER assume without verification:**
- Don't skip code sections
- Don't make assumptions about missing files
- Don't rely on file names alone
- Always trace data flows end-to-end

**ALWAYS generate three complementary outputs:**
1. **JSON** — Graph-based structured data (nodes, edges, data flows, dependencies)
2. **Markdown** — Human-readable documentation with details
3. **TUI** — Interactive terminal explorer for browsing structure

**Language Support Guaranteed:**
- JavaScript/TypeScript, Python, Go, Java, PHP, Ruby, C#, Rust (built-in patterns)
- Any other language via language-agnostic pattern detection
- Auto-detection requires zero configuration

---

## Core Mindset

Think like an **application security auditor**:

```
┌─────────────────────────────────────────────────────────────┐
│ ANALYSIS APPROACH                                             │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│ • THOROUGHNESS: Examine every component systematically      │
│ • CURIOSITY: Question every design choice and trust         │
│ • CONTEXT: Understand the business purpose first            │
│ • RIGOR: Verify findings against actual code                │
│ • COMPLETENESS: Leave no stone unturned                     │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## Analysis Methodology

### Phase 1: Reconnaissance

**Examine all inputs systematically:**

```
┌─────────────────────────────────────────────────────────────┐
│ INFORMATION GATHERING                                        │
├─────────────────────────────────────────────────────────────┤
│ 1. PROJECT CONTEXT                                           │
│    - Application name and purpose                            │
│    - Technology stack and frameworks                         │
│    - Architecture style (monolith, microservices, API, etc.)│
│                                                              │
│ 2. SOURCE CODE ANALYSIS                                      │
│    - Read EVERY file (entry points first)                    │
│    - Identify modules and their relationships                │
│    - Extract user-facing features                            │
│    - Trace data flow paths                                   │
│    - Note security-sensitive operations                      │
│                                                              │
│ 3. FEATURE EXTRACTION                                        │
│    - User roles and role hierarchy                           │
│    - Permissions and access control model                    │
│    - Authentication mechanisms and flows                     │
│    - API endpoints and methods                               │
│    - Data models and entity relationships                    │
│    - Workflows and business processes                        │
│                                                              │
│ 4. DEPENDENCY MAPPING                                        │
│    - Service-to-service calls                                │
│    - External service dependencies                           │
│    - Data flow between components                            │
│    - Trust boundaries                                        │
└─────────────────────────────────────────────────────────────┘
```

### Phase 2: Domain Identification

**Separate concerns into logical domains:**

```
TYPICAL DOMAINS:
├─ Authentication & Authorization
│  ├─ User roles and role hierarchy
│  ├─ Permission system (RBAC, ACL, capability-based)
│  ├─ Authentication methods (JWT, session, OAuth, API key)
│  └─ Access control enforcement points
│
├─ Content/Data Management
│  ├─ Content types and models
│  ├─ CRUD operations
│  ├─ Publishing workflows
│  └─ Data validation
│
├─ User Management
│  ├─ User profiles
│  ├─ Account creation/modification
│  ├─ Admin functions
│  └─ Audit logging
│
├─ Payment/Commerce (if applicable)
│  ├─ Payment processing
│  ├─ Order management
│  ├─ Billing workflows
│  └─ PCI compliance requirements
│
└─ [Custom Domain]
   └─ Any domain specific to the application
```

### Phase 3: Feature Extraction

**For each domain, extract these feature types:**

| Feature Type | Examples | Security Relevance |
|--------------|----------|-------------------|
| **Roles** | Admin, Editor, Author, Viewer | Authorization boundary |
| **Permissions** | read, write, delete, publish, manage_users | Access control policy |
| **Authentication** | JWT, Session, OAuth, API Key, WebAuthn | Identity verification |
| **Endpoints** | REST, GraphQL, RPC, WebSocket, gRPC | Attack surface |
| **Data Models** | User, Post, Product, Transaction | Data sensitivity |
| **Workflows** | Login, Publishing, Payment, Approval | Business logic risk |
| **Data Flows** | Credential → Auth → Token | Sensitive paths |
| **Dependencies** | Internal, external services | Failure points |

### Phase 4: Risk Assessment

**Identify security-sensitive components:**

```
RISK FACTORS:
├─ AUTHENTICATION & AUTHORIZATION
│  ├─ Weak password policy
│  ├─ Missing MFA implementation
│  ├─ Insufficient permission checks
│  └─ Session management flaws
│
├─ DATA HANDLING
│  ├─ Unvalidated user input
│  ├─ SQL/command injection vectors
│  ├─ Sensitive data in logs
│  └─ Missing encryption
│
├─ API SECURITY
│  ├─ Missing authentication
│  ├─ Rate limiting absent
│  ├─ CORS misconfigurations
│  └─ Unvalidated redirects
│
├─ ADMIN FUNCTIONS
│  ├─ Privilege escalation vectors
│  ├─ Insufficient audit logging
│  ├─ Missing input validation
│  └─ No rate limiting
│
└─ EXTERNAL INTEGRATIONS
   ├─ Unvalidated webhooks
   ├─ API key exposure
   ├─ Insecure service communication
   └─ Dependency vulnerabilities
```

---

## Usage

### Inputs

Provide source code via:
- Directory path (entire codebase or subset)
- Individual files
- Repository structure
- Code snippets (for partial analysis)

### Outputs: Three Complementary Formats

**ALL THREE are always generated:**

#### OUTPUT 1: JSON (Graph-Based Structure)

Complete relationship graph with nodes, edges, and data flows:

```json
{
  "app_metadata": {
    "name": "Application Name",
    "language": "Python",
    "type": "Web Application",
    "complexity_score": 7.5,
    "total_domains": 5,
    "total_flows": 12,
    "total_endpoints": 20
  },
  "domains": [
    {
      "id": "auth",
      "name": "Authentication & Authorization",
      "features": [
        {
          "id": "roles",
          "type": "role_system",
          "name": "User Roles",
          "items": [
            {"name": "Admin", "permissions": ["read", "write", "delete", "manage_users"]},
            {"name": "Editor", "permissions": ["read", "write", "publish"]},
            {"name": "Viewer", "permissions": ["read"]}
          ],
          "risk_level": "high"
        }
      ],
      "risk_areas": ["Session management", "Token validation", "Permission enforcement"]
    }
  ],
  "graph": {
    "nodes": [
      {"id": "auth_domain", "type": "domain", "label": "Authentication", "risk_level": "high"},
      {"id": "content_domain", "type": "domain", "label": "Content", "risk_level": "low"}
    ],
    "edges": [
      {
        "source": "content_domain",
        "target": "auth_domain",
        "type": "depends_on",
        "label": "requires auth for access control"
      }
    ]
  },
  "data_flows": [
    {
      "source": "POST /api/login",
      "destination": "Auth Service",
      "data_type": "user_credentials",
      "sensitivity": "critical",
      "encryption": "TLS_1_3"
    }
  ],
  "dependencies": {
    "internal": [...],
    "external": [...]
  }
}
```

**Graph Components:**
- `nodes` — Domains, features, flows, endpoints
- `edges` — Connections (dependency, permission_check, depends_on, calls, triggers, uses)
- `data_flows` — Sensitive data movement (source → destination)
- `dependencies` — Internal (domain-to-domain) and external (service) relationships

#### OUTPUT 2: Markdown (Human-Readable Documentation)

Complete application documentation including:
- Executive summary
- Domain descriptions
- Feature lists with risk levels
- User workflow documentation
- Data flow diagrams (text-based)
- Risk area annotations
- Recommendations

#### OUTPUT 3: TUI (Interactive Terminal Explorer)

Keyboard-navigable application map:

```
┌─ Application Map ────────────────────────────────────┐
│                                                      │
│ ▼ Authentication & Authorization         [HIGH]    │
│   ├─ ▼ User Roles                        [5 roles] │
│   │   ├─ Admin [manage all]                        │
│   │   ├─ Editor [edit content]                     │
│   │   └─ Viewer [read only]                        │
│   ├─ JWT Authentication                 [connected]│
│   └─ Session Management                 [1 flow]  │
│ ▶ Content Management                     [LOW]     │
│ ▶ User Management                        [MEDIUM]  │
│                                                      │
│ [↑↓] navigate | [→←] expand | [/] search | [?] help│
│ High-risk: 4 | Total flows: 8 | Commands: c,d,f,s │
└──────────────────────────────────────────────────────┘
```

**TUI Commands:**
```
Navigation:     ↑/↓ move, ←/→ collapse/expand, Home/End
View Modes:     t=tree, f=flows, c=connections, d=data-flows, s=stats
Filtering:      / search,  h=high-risk, m=medium, l=low, a=all
Actions:        Enter=details, q=quit, ?=help
```

---

## Detection Capabilities

### Language Support

**Built-in Pattern Recognition:**
- JavaScript/TypeScript (Express, Next.js, Fastify, NestJS, Koa)
- Python (Django, Flask, FastAPI, Pyramid, Bottle)
- Go (standard library, Gin, Echo, gRPC, Fiber)
- Java/Kotlin (Spring, Spring Boot, Micronaut, Quarkus)
- PHP (Laravel, Symfony, WordPress, Slim)
- Ruby (Rails, Sinatra, Hanami, Grape)
- C# (.NET, ASP.NET Core, ServiceStack)
- Rust (Actix, Rocket, Axum, Actix-web)

**Language-Agnostic Detection:**
- Pattern-based analysis works regardless of language
- Auto-detects from file structure and syntax patterns
- Zero configuration required

---

## What Gets Detected

```
FEATURE CATEGORIES:

1. ROLE & PERMISSION SYSTEMS
   ├─ Role definitions (Admin, Editor, Author, Viewer, etc.)
   ├─ Permission matrices
   ├─ Role hierarchies and inheritance
   └─ Access control model (RBAC, ACL, ABAC)

2. AUTHENTICATION MECHANISMS
   ├─ JWT tokens
   ├─ Session-based auth
   ├─ OAuth / OpenID Connect
   ├─ SAML
   ├─ API Keys
   └─ WebAuthn / MFA

3. DATA MODELS & TYPES
   ├─ User entities
   ├─ Content types (Posts, Pages, Products, etc.)
   ├─ Relationships between entities
   ├─ Database schema patterns
   └─ Data sensitivity levels

4. API ENDPOINTS
   ├─ HTTP methods (GET, POST, PUT, DELETE, PATCH)
   ├─ REST vs GraphQL vs RPC patterns
   ├─ Required authentication/authorization
   ├─ Input validation patterns
   └─ Error handling approaches

5. USER WORKFLOWS
   ├─ Login flow
   ├─ Content creation → Review → Publish
   ├─ Payment processing flow
   ├─ User registration and onboarding
   └─ Admin operations

6. DATA FLOWS
   ├─ Credential transmission
   ├─ User input → Processing → Output
   ├─ Database interactions
   └─ Service-to-service communication

7. RISK-SENSITIVE OPERATIONS
   ├─ File uploads / downloads
   ├─ Payment processing
   ├─ Admin functions
   ├─ Privilege escalation vectors
   └─ Sensitive data access
```

---

## Success Criteria

**Analysis is complete when:**

```
┌─────────────────────────────────────────────────────────────┐
│ COMPLETION CHECKLIST                                         │
├─────────────────────────────────────────────────────────────┤
│ ✓ All source files examined                                  │
│ ✓ Complete domain map created                                │
│ ✓ All user roles identified                                  │
│ ✓ All permissions documented                                 │
│ ✓ Authentication methods listed                              │
│ ✓ All endpoints mapped                                       │
│ ✓ User workflows documented                                  │
│ ✓ Data flows traced end-to-end                               │
│ ✓ Risk areas flagged and annotated                           │
│ ✓ Dependencies (internal & external) identified              │
│ ✓ JSON graph generated with all relationships                │
│ ✓ Markdown documentation complete                            │
│ ✓ TUI explorer functional and browsable                      │
│ ✓ Findings validated against actual source code              │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

**Do not stop until:**
1. All domains and features are documented
2. All risk areas are identified and annotated
3. Both high-level AND detailed views are complete
4. Outputs are accurate and reproducible

---

## Analysis Documentation Template

**After completing analysis, provide findings in this format:**

```markdown
## Application Analysis: [Application Name]

**Metadata:**
- Language: [Programming Language]
- Type: [Web App / API / Microservice / etc]
- Complexity Score: [1-10]
- Total Domains: [N]
- Total Features: [N]

### Domain Overview
[List of all identified domains with brief descriptions]

### Authentication & Authorization
- **Model**: [RBAC / ACL / ABAC / Custom]
- **Roles**: [List all roles]
- **Permissions**: [List all permissions]
- **Auth Methods**: [JWT / Session / OAuth / etc]
- **Risk Areas**: [Identified vulnerabilities]

### [Domain Name]
- **Purpose**: [What this domain does]
- **Features**: [List of features]
- **Workflows**: [Workflows in this domain]
- **Risk Level**: [HIGH / MEDIUM / LOW]
- **Concerns**: [Identified risks]

### Data Flows
[Critical data paths and their sensitivity levels]

### Dependencies
- **Internal**: [Domain-to-domain relationships]
- **External**: [Services this application depends on]

### Security Summary
[High-level assessment of security posture]

### Recommendations
[Suggested areas for security testing or improvement]

---

### Full JSON Graph
[Complete graph-based representation for programmatic analysis]
```

---

## Approach Summary

```
ANALYSIS PROCESS:

1. READ all source code carefully
   └─ Entry points first, then supporting modules
   
2. MAP the application structure
   └─ Identify domains and their relationships
   
3. EXTRACT features systematically
   ├─ User roles and permissions
   ├─ Authentication mechanisms
   ├─ API endpoints and methods
   ├─ Data models and relationships
   └─ Workflows and business logic
   
4. IDENTIFY security-sensitive areas
   └─ Flag high-risk components for further testing
   
5. GENERATE three complementary outputs
   ├─ JSON (for Hacktron integration)
   ├─ Markdown (for documentation)
   └─ TUI (for interactive exploration)
   
6. VALIDATE findings against source code
   └─ Ensure accuracy and completeness
   
7. DOCUMENT the analysis
   └─ Use standard template for consistency
```

---

## Integration Points

**Use analysis results with:**

| Tool | Use Case | Input Format |
|------|----------|--------------|
| **Hacktron** | Autonomous vulnerability testing | JSON (filter by risk_level: "high") |
| **D3.js / Cytoscape** | Architecture visualization | JSON graph (nodes/edges) |
| **Threat Modeling** | Security assessment | Markdown + identified risks |
| **Team Wiki** | Documentation & onboarding | Markdown output |
| **CI/CD Pipeline** | Continuous architecture monitoring | JSON for version comparison |
