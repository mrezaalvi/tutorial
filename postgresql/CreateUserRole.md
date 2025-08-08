Linux/Ubuntu
1. Pada terminal, masukkan command berikut:

    ```bash
    sudo -u postgres psql
    ```

2. Membuat Role Tanpa Login (Role Murni)
    
    ```bash
    CREATE ROLE nama_role;
    ```

    contoh:

    ```bash
    CREATE ROLE dbadmin;
    ```

    Role ini tidak bisa login, biasanya dipakai untuk pengelompokan hak akses.

3. Membuat User (Role dengan Login)

    ```bash
    CREATE ROLE nama_user WITH LOGIN PASSWORD 'passwordku';
    ```

    Atau pakai kata kunci CREATE USER (shortcut dari CREATE ROLE ... WITH LOGIN):

    ```bash
    CREATE USER nama_user WITH PASSWORD 'passwordku';
    ```

4. Menentukan Hak Akses
   - Berikan hak membuat database

        ```bash
        ALTER ROLE nama_user CREATEDB;
        ```

   - Berikan hak membuat role lain

        ```bash
        ALTER ROLE nama_user CREATEROLE;
        ```

   - Jadikan superuser

        ```bash
        ALTER ROLE nama_user SUPERUSER;
        ```
    
    ⚠️ Gunakan superuser hanya untuk admin.

5. Mengatur Role Default (Opsional)
    
    Misalnya, kita punya role read_only yang punya hak SELECT saja:

    ```bash
    CREATE ROLE read_only;
    GRANT CONNECT ON DATABASE namadb TO read_only;
    GRANT USAGE ON SCHEMA public TO read_only;
    GRANT SELECT ON ALL TABLES IN SCHEMA public TO read_only;
    ```

6. Cek User/Role yang Ada

    ```bash
    \du
    ```