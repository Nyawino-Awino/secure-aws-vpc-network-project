# 🧪 Break & Fix Troubleshooting Lab

This section documents real-world issues simulated and resolved during the project.

---

## ❌ Scenario 1: Website Not Loading

### Issue:
HTTP access (port 80) was removed from the web server security group.

### Impact:
- Website became inaccessible from the browser

### Root Cause:
- Missing inbound HTTP rule in Security Group

### Fix:
- Added HTTP (port 80) rule allowing traffic from 0.0.0.0/0

---

## ❌ Scenario 2: No Internet Access

### Issue:
Route to Internet Gateway was removed from the public route table.

### Impact:
- Web server could not be accessed externally

### Root Cause:
- Missing default route (0.0.0.0/0 → IGW)

### Fix:
- Restored route to Internet Gateway in route table

---

## ❌ Scenario 3: Database Connection Failure

### Issue:
Database security group was misconfigured.

### Impact:
- Web server could not connect to database

### Root Cause:
- MySQL port (3306) not restricted correctly

### Fix:
- Allowed access only from web server security group

---

## 🧠 Troubleshooting Approach

1. Identify symptoms (what is failing)
2. Check infrastructure layer:
   - Compute (EC2)
   - Network (VPC, routing)
   - Security (SG, NACL)
3. Validate configurations
4. Apply fix and retest
