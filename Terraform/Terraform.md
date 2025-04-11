# Terraform Coding Standards

## 1. Overview
Terraform is the default tool used for provisioning cloud infrastructure. This guide defines the coding standards and best practices for writing and maintaining Terraform scripts.

---

## 2. Versions
- The currently supported version of Terraform is:  
   ```terraform
   0.12
   ```

---

## 3. Formatting and Style

### 3.1 Indentation and Spacing
- Use **2 spaces** for indentation (not tabs).
- Consistent spacing aids readability and code consistency.

### 3.2 Alignment
- Ensure all code is **correctly and consistently aligned** for better legibility.

### 3.3 Naming Conventions
- Use **snake_case** for all element names to avoid Terraform warnings:
    - ✅ `my_resource`  
    - ❌ `my-resource`  

---

## 4. Modules

### 4.1 Module Structure
- When your scripts are sufficiently large, use modules to promote reusability and maintainability.
- Each module should reside in its own directory, following the naming convention:  
   ```plaintext
   module-<FUNCTION>
   ```
- Example:
    - ✅ `module-security-groups`
    - ✅ `module-ec2-instances`

---

## 5. Comments and Descriptions

### 5.1 Comments
- **Minimise comments** where possible. Code should be self-explanatory.  
- Use **descriptions** instead of comments where supported, as descriptions are visible in the AWS console.

### 5.2 Example
```terraform
# Avoid comments like this
# This security group allows SSH access
resource "aws_security_group" "ssh" {
  description = "Allows SSH access"
  ...
}
```

---

## 6. Resources

### 6.1 Resource Naming
- Use **snake_case** for all resource names:
    - ✅ `my_instance`
    - ❌ `my-instance`
- This prevents Terraform warnings and maintains consistency.

---
