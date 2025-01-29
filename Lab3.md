# Lab Demo: Using Schemas in Postgre

`Let’s go through a quick demo where we use schemas to organize tables for an application.`

- **Step 1: Create a Schema**

```sql
-- Create a new schema for a blog application
CREATE SCHEMA blog;
```

- **Step 2: Create Tables in the Schema**

```sql
-- Create tables inside the blog schema
CREATE TABLE blog.posts (
  post_id SERIAL PRIMARY KEY,
  title VARCHAR(200),
  content TEXT,
  author_id INT
);

CREATE TABLE blog.comments (
  comment_id SERIAL PRIMARY KEY,
  post_id INT REFERENCES blog.posts(post_id),
  commenter_name VARCHAR(100),
  comment_text TEXT
);
```


- **Step 3: Insert Data into the Tables**

```sql
-- Insert a new post
INSERT INTO blog.posts (title, content, author_id)
VALUES ('First Post', 'This is my first blog post.', 1);

-- Insert a comment for the post
INSERT INTO blog.comments (post_id, commenter_name, comment_text)
VALUES (1, 'Jane Doe', 'Great post!');

```

- **Step 4: Query Data from the Tables**

```sql
-- Query the posts from the blog schema
SELECT * FROM blog.posts;

-- Query the comments for a specific post
SELECT * FROM blog.comments WHERE post_id = 1;
```

- **Step 5: Drop the Schema (If Needed)**

```sql
-- Drop the schema and all the objects within it
DROP SCHEMA blog CASCADE;
```

---

- Learning : PostgreSQL, schemas provide a powerful way to logically organize your database objects. You can have multiple schemas within a single database, which helps in managing complex applications and avoiding naming conflicts. 