# Store Management

Stock management web application developed with **Symfony 7.4**.

## Description

This project allows you to manage:
- **categories**,
- **products**,
- **stock movements** (in/out),
- **low-stock replenishment tracking**.

Authentication is built with Symfony Security, including role-based access control.

## Main Features

- User login / logout.
- Roles: `ROLE_EMPLOYE` and `ROLE_ADMIN`.
- Full CRUD for:
  - Categories
  - Products
  - Stock movements
- Automatic stock updates when creating/editing stock movements.
- Insufficient stock check for outgoing movements.
- Replenishment view (products where stock is less than or equal to alert threshold).
- CSRF protection on sensitive forms.

## Tech Stack

- PHP `>= 8.2`
- Symfony `7.4`
- Doctrine ORM
- Twig
- Bootstrap / Bootswatch (Minty)
- MySQL (current configuration in `.env`)

## Project Setup

### 1) Clone the repository

```bash
git clone <REPO_URL>
cd gestion_magasin
```

### 2) Install dependencies

```bash
composer install
```

### 3) Configure the database

The current variable in `.env` is:

```dotenv
DATABASE_URL="mysql://root:@127.0.0.1:3307/gestion_magasin_db"
```

Adjust this value to match your local environment (XAMPP / local MySQL).

### 4) Create the database and schema

```bash
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
```

If no migration files are available in your repository, run:

```bash
php bin/console doctrine:schema:update --force
```

### 5) (Optional) Load fixtures

```bash
php bin/console doctrine:fixtures:load
```

> Current fixtures mainly add categories.

## User Creation (admin/employee)

This project does not include ready-to-use user fixtures.

1. Generate a hashed password:

```bash
php bin/console security:hash-password
```

2. Insert a user in the `user` table (SQL example):

```sql
INSERT INTO user (email, roles, password)
VALUES ('admin@magasin.local', '["ROLE_ADMIN"]', '<HASHED_PASSWORD>');
```

Employee example:

```sql
INSERT INTO user (email, roles, password)
VALUES ('employe@magasin.local', '["ROLE_EMPLOYE"]', '<HASHED_PASSWORD>');
```

## Run the Application

With Symfony CLI:

```bash
symfony server:start
```

Or with native PHP:

```bash
php -S 127.0.0.1:8000 -t public
```

Then open:
- `http://127.0.0.1:8000/login`

## Useful Routes

- `/login`
- `/home`
- `/categorie`
- `/produit`
- `/produit/reapprovisionnement`
- `/mouvement/stock`

## Simplified Structure

- `src/Entity`: Doctrine entities (`Categorie`, `Produit`, `MouvementStock`, `User`)
- `src/Controller`: MVC controllers
- `src/Form`: Symfony forms
- `templates/`: Twig views
- `config/packages/security.yaml`: security and access configuration

## GitHub Publishing

If not done yet:

```bash
git init
git add .
git commit -m "Initial commit - store management"
git branch -M main
git remote add origin <GITHUB_URL>
git push -u origin main
```

## Authors

- Amine RACHID
- Saad Farhi

---

Project developed as part of a dynamic web development module using PHP/Symfony.
=======
# Store-Management
Symfony 7.4 inventory management web app with role-based authentication, product/category CRUD, stock movement tracking, and low-stock replenishment alerts.
