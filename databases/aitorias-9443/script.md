# Script SQL para implementación de la base de datos para el blog

```sql
-- Check if the database exists
IF NOT EXISTS (SELECT 1 FROM sys.databases WHERE name = 'blog')
BEGIN
    -- Create the database
    CREATE DATABASE blog;
END;

-- Use the newly created database
USE blog;

-- Check if the users table exists
IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'users')
BEGIN
    -- Create table users
    CREATE TABLE users (
        id int NOT NULL AUTO_INCREMENT,
        first_name varchar(100) NOT NULL,
        last_name varchar(100) NOT NULL,
        birth_date date,
        email varchar(50),
        password varchar(16),
        created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP on update CURRENT_TIMESTAMP,
        role_id int,
        PRIMARY KEY (id),
        KEY role_id_xid (role_id)
    );
END;

-- Check if the roles table exists
IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'roles')
BEGIN
    -- Create table roles
    CREATE TABLE roles (
        id int NOT NULL AUTO_INCREMENT,
        name varchar(100) NOT NULL,
        created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP on update CURRENT_TIMESTAMP,
        PRIMARY KEY (id)
    );
END;

-- Check if the posts table exists
IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'posts')
BEGIN
    -- Create table posts
    CREATE TABLE posts (
        id int NOT NULL AUTO_INCREMENT,
        title varchar(255) NOT NULL,
        content text NOT NULL,
        thumbnail varchar(255),
        created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP on update CURRENT_TIMESTAMP,
        user_id int,
        category_id int,
        PRIMARY KEY (id),
        KEY user_id_xid (user_id),
        KEY category_id_xid (category_id)
    );
END;

-- Check if the comments table exists
IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'comments')
BEGIN
    -- Create table comments
    CREATE TABLE comments (
        id int NOT NULL AUTO_INCREMENT,
        content text NOT NULL,
        created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP on update CURRENT_TIMESTAMP,
        user_id int,
        article_id int,
        PRIMARY KEY (id),
        KEY user_id_xid (user_id),
        KEY article_id_xid (article_id)
    );
END;

-- Check if the categories table exists
IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'categories')
BEGIN
    -- Create table categories
    CREATE TABLE categories (
        id int NOT NULL AUTO_INCREMENT,
        name varchar(255) NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP on update CURRENT_TIMESTAMP,
        PRIMARY KEY (id)
    );
END;

-- Check if the postsCategories table exists
IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'postsCategories')
BEGIN
    -- Create table postsCategories
    CREATE TABLE postsCategories (
        id int NOT NULL AUTO_INCREMENT,
        post_id int,
        category_id int,
        PRIMARY KEY (id),
        KEY post_id_xid (post_id),
        KEY category_id_xid (category_id)
    );
END;

-- Check if the tags table exists
IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'tags')
BEGIN
    -- Create table tags
    CREATE TABLE tags (
        id int NOT NULL AUTO_INCREMENT,
        name varchar(255) NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP on update CURRENT_TIMESTAMP,
        PRIMARY KEY (id)
    );
END;

-- Check if the postsTags table exists
IF NOT EXISTS (SELECT 1 FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_NAME = 'postsTags')
BEGIN
    -- Create table postsTags
    CREATE TABLE postsTags (
        id int NOT NULL AUTO_INCREMENT,
        post_id int,
        tag_id int,
        PRIMARY KEY (id),
        KEY post_id_xid (post_id),
        KEY tag_id_xid (tag_id)
    );
END;
```