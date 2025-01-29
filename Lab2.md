```markdown
PostgreSQL Administration: Creating and Managing Users and Roles
```
## Introduction
Managing users and roles is a fundamental task in PostgreSQL administration. This tutorial will guide you through creating, managing, and securing database users and roles in PostgreSQL.

---

## Prerequisites
- PostgreSQL installed and running.
- Access to the PostgreSQL database as a superuser (e.g., `postgres`).

---

## Key Concepts

### Users vs. Roles
- **Roles** in PostgreSQL can function as users or groups, depending on their configuration.
- A **user** is essentially a role with the ability to log in (`LOGIN` privilege).
- Roles can have permissions assigned and can also inherit permissions from other roles.

---

## 1. Connecting to PostgreSQL
To manage users and roles, first connect to your PostgreSQL server using the `psql` tool:

```bash
psql -U postgres -d postgres
```

---

## 2. Creating Users and Roles

### 2.1 Creating a Role
A basic role can be created using the `CREATE ROLE` command.

```sql
CREATE ROLE my_role;
```

### 2.2 Creating a User
To create a user with login privileges, use the `CREATE USER` command:

```sql
CREATE USER my_user WITH PASSWORD 'secure_password';
```

### 2.3 Creating a Role with Additional Options
You can create a role with specific privileges, such as creating databases or assigning roles:

```sql
CREATE ROLE admin_role WITH LOGIN CREATEDB CREATEROLE PASSWORD 'admin_password';
```

---

## 3. Managing Roles

### 3.1 Granting Privileges to a Role
Use the `GRANT` command to assign privileges to a role.

#### Granting All Privileges on a Database
```sql
GRANT ALL PRIVILEGES ON DATABASE my_database TO my_role;
```

#### Granting Specific Table Privileges
```sql
GRANT SELECT, INSERT ON TABLE my_table TO my_role;
```

### 3.2 Revoking Privileges
To remove privileges, use the `REVOKE` command:

```sql
REVOKE INSERT ON TABLE my_table FROM my_role;
```

---

## 4. Managing Users

### 4.1 Altering a User
To modify a user, use the `ALTER ROLE` command:

#### Changing a User’s Password
```sql
ALTER ROLE my_user WITH PASSWORD 'new_password';
```

#### Adding a Privilege
```sql
ALTER ROLE my_user WITH CREATEDB;
```

#### Removing a Privilege
```sql
ALTER ROLE my_user NOLOGIN;
```

### 4.2 Dropping a User
To delete a user or role, ensure that it does not own any database objects or have active sessions:

```sql
DROP ROLE my_user;
```

---

## 5. Using Role Inheritance
Roles in PostgreSQL can inherit privileges from other roles.

### 5.1 Creating a Parent Role
```sql
CREATE ROLE parent_role WITH CREATEDB;
```

### 5.2 Creating a Child Role
```sql
CREATE ROLE child_role INHERIT;
GRANT parent_role TO child_role;
```

### 5.3 Verifying Inherited Privileges
Login as `child_role` to verify that it inherits the privileges of `parent_role`.

---

## 6. Best Practices
1. Use **strong passwords** for all users.
2. Grant the **minimum privileges** required for each role.
3. Regularly audit user privileges and roles.
4. Use **role inheritance** to simplify privilege management.
5. Avoid using the `postgres` superuser account for day-to-day tasks.

---

## 7. Hands-On Lab

### Scenario
1. Create a user `developer` with login privileges.
2. Create a role `readonly` with `SELECT` privileges on the `employees` table.
3. Assign `readonly` role to `developer`.
4. Verify that the `developer` user can only query the `employees` table.

#### Step 1: Create User
```sql
CREATE USER developer WITH PASSWORD 'dev_password';
```

#### Step 2: Create Role
```sql
CREATE ROLE readonly;
GRANT SELECT ON TABLE employees TO readonly;
```

#### Step 3: Assign Role to User
```sql
GRANT readonly TO developer;
```

#### Step 4: Verify Access
1. Login as `developer`:
   ```bash
   psql -U developer -d your_database
   ```
2. Run a `SELECT` query on the `employees` table:
   ```sql
   SELECT * FROM employees;
   ```
3. Try running an `INSERT` query (it should fail):
   ```sql
   INSERT INTO employees (id, name) VALUES (1, 'Test');
   ```

---

## Conclusion
In this tutorial, you’ve learned how to create and manage users and roles in PostgreSQL. You also explored role inheritance, privilege management, and some best practices to secure your PostgreSQL environment.
