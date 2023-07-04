## Script SQL para crear las tablas

```sql
-- Tabla Usuario
CREATE TABLE Usuario (
    id_usuario INT PRIMARY KEY,
    nombre VARCHAR(50),
    correo_electronico VARCHAR(50),
    contraseña VARCHAR(50)
);

-- Tabla Artículo
CREATE TABLE Artículo (
    id_articulo INT PRIMARY KEY,
    título VARCHAR(100),
    contenido TEXT,
    fecha_publicacion DATE,
    id_usuario INT,
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);

-- Tabla Comentario
CREATE TABLE Comentario (
    id_comentario INT PRIMARY KEY,
    contenido TEXT,
    fecha_publicacion DATE,
    id_articulo INT,
    id_usuario INT,
    FOREIGN KEY (id_articulo) REFERENCES Artículo(id_articulo),
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);