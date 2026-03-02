# Autor : Angel Santiago Hernandez 
# PRUEBA TECNICA DEVSU

# Desafio

https://github.com/sangelAng17/devSu-Cliente/blob/main/README.md


# Requisitos

 - openjdk version "17.0.2" 2022-01-18
 - OpenJDK Runtime Environment (build 17.0.2+8-86)
 - OpenJDK 64-Bit Server VM (build 17.0.2+8-86, mixed mode, sharing)
 - Postgress

# Instalacion
Clonar los repositorios

 - https://github.com/sangelAng17/devSu-Cliente/tree/main
 - https://github.com/sangelAng17/devSu-Cuenta/tree/main

# DIAGRAMA ENTIDAD RELACION 


<img width="909" height="658" alt="diagrama" src="https://github.com/user-attachments/assets/171fafbd-f07f-43cf-90a4-5bfe91a5b8eb" />


# DLL DATABASE

```SQL
-- DROP SCHEMA public;

CREATE SCHEMA public AUTHORIZATION postgres;

COMMENT ON SCHEMA public IS 'standard public schema';

-- DROP SEQUENCE public.cliente_id_seq;

CREATE SEQUENCE public.cliente_id_seq
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 9223372036854775807
	START 1
	CACHE 1
	NO CYCLE;

-- Permissions

ALTER SEQUENCE public.cliente_id_seq OWNER TO postgres;
GRANT ALL ON SEQUENCE public.cliente_id_seq TO postgres;

-- DROP SEQUENCE public.cuenta_id_seq;

CREATE SEQUENCE public.cuenta_id_seq
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 9223372036854775807
	START 1
	CACHE 1
	NO CYCLE;

-- Permissions

ALTER SEQUENCE public.cuenta_id_seq OWNER TO postgres;
GRANT ALL ON SEQUENCE public.cuenta_id_seq TO postgres;

-- DROP SEQUENCE public.estado_id_seq;

CREATE SEQUENCE public.estado_id_seq
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 9223372036854775807
	START 1
	CACHE 1
	NO CYCLE;

-- Permissions

ALTER SEQUENCE public.estado_id_seq OWNER TO postgres;
GRANT ALL ON SEQUENCE public.estado_id_seq TO postgres;

-- DROP SEQUENCE public.genero_id_seq;

CREATE SEQUENCE public.genero_id_seq
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 9223372036854775807
	START 1
	CACHE 1
	NO CYCLE;

-- Permissions

ALTER SEQUENCE public.genero_id_seq OWNER TO postgres;
GRANT ALL ON SEQUENCE public.genero_id_seq TO postgres;

-- DROP SEQUENCE public.movimiento_id_seq;

CREATE SEQUENCE public.movimiento_id_seq
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 9223372036854775807
	START 1
	CACHE 1
	NO CYCLE;

-- Permissions

ALTER SEQUENCE public.movimiento_id_seq OWNER TO postgres;
GRANT ALL ON SEQUENCE public.movimiento_id_seq TO postgres;

-- DROP SEQUENCE public.persona_id_seq;

CREATE SEQUENCE public.persona_id_seq
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 9223372036854775807
	START 1
	CACHE 1
	NO CYCLE;

-- Permissions

ALTER SEQUENCE public.persona_id_seq OWNER TO postgres;
GRANT ALL ON SEQUENCE public.persona_id_seq TO postgres;

-- DROP SEQUENCE public.tipo_cuenta_id_seq;

CREATE SEQUENCE public.tipo_cuenta_id_seq
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 9223372036854775807
	START 1
	CACHE 1
	NO CYCLE;

-- Permissions

ALTER SEQUENCE public.tipo_cuenta_id_seq OWNER TO postgres;
GRANT ALL ON SEQUENCE public.tipo_cuenta_id_seq TO postgres;

-- DROP SEQUENCE public.tipo_movimiento_id_seq;

CREATE SEQUENCE public.tipo_movimiento_id_seq
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 9223372036854775807
	START 1
	CACHE 1
	NO CYCLE;

-- Permissions

ALTER SEQUENCE public.tipo_movimiento_id_seq OWNER TO postgres;
GRANT ALL ON SEQUENCE public.tipo_movimiento_id_seq TO postgres;
-- public.estado definition

-- Drop table

-- DROP TABLE public.estado;

CREATE TABLE public.estado (
	id int8 GENERATED ALWAYS AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 9223372036854775807 START 1 CACHE 1 NO CYCLE) NOT NULL,
	descripcion varchar NULL,
	CONSTRAINT estado_pk PRIMARY KEY (id)
);

-- Permissions

ALTER TABLE public.estado OWNER TO postgres;
GRANT ALL ON TABLE public.estado TO postgres;


-- public.genero definition

-- Drop table

-- DROP TABLE public.genero;

CREATE TABLE public.genero (
	id int8 GENERATED ALWAYS AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 9223372036854775807 START 1 CACHE 1 NO CYCLE) NOT NULL,
	descripcion varchar NULL,
	CONSTRAINT genero_pk PRIMARY KEY (id)
);

-- Permissions

ALTER TABLE public.genero OWNER TO postgres;
GRANT ALL ON TABLE public.genero TO postgres;


-- public.tipo_cuenta definition

-- Drop table

-- DROP TABLE public.tipo_cuenta;

CREATE TABLE public.tipo_cuenta (
	id int8 GENERATED ALWAYS AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 9223372036854775807 START 1 CACHE 1 NO CYCLE) NOT NULL,
	descripcion varchar NULL,
	CONSTRAINT tipo_cuenta_pk PRIMARY KEY (id)
);

-- Permissions

ALTER TABLE public.tipo_cuenta OWNER TO postgres;
GRANT ALL ON TABLE public.tipo_cuenta TO postgres;


-- public.tipo_movimiento definition

-- Drop table

-- DROP TABLE public.tipo_movimiento;

CREATE TABLE public.tipo_movimiento (
	id int8 GENERATED ALWAYS AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 9223372036854775807 START 1 CACHE 1 NO CYCLE) NOT NULL,
	descripcion varchar NULL,
	CONSTRAINT tipo_movimiento_pk PRIMARY KEY (id)
);

-- Permissions

ALTER TABLE public.tipo_movimiento OWNER TO postgres;
GRANT ALL ON TABLE public.tipo_movimiento TO postgres;


-- public.persona definition

-- Drop table

-- DROP TABLE public.persona;

CREATE TABLE public.persona (
	id int8 GENERATED ALWAYS AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 9223372036854775807 START 1 CACHE 1 NO CYCLE) NOT NULL,
	nombre varchar NULL,
	id_genero_pk int8 NULL,
	edad int4 NULL,
	identifiacion numeric NULL,
	direccion varchar NULL,
	telefono numeric NULL,
	CONSTRAINT newtable_pk PRIMARY KEY (id),
	CONSTRAINT fk_persona_genero FOREIGN KEY (id_genero_pk) REFERENCES public.genero(id)
);

-- Permissions

ALTER TABLE public.persona OWNER TO postgres;
GRANT ALL ON TABLE public.persona TO postgres;


-- public.cliente definition

-- Drop table

-- DROP TABLE public.cliente;

CREATE TABLE public.cliente (
	id int8 GENERATED ALWAYS AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 9223372036854775807 START 1 CACHE 1 NO CYCLE) NOT NULL,
	"password" varchar NULL,
	id_estado_pk int8 NULL,
	id_persona_pk int8 NOT NULL,
	CONSTRAINT cliente_pk PRIMARY KEY (id),
	CONSTRAINT fk_cliente_estado FOREIGN KEY (id_estado_pk) REFERENCES public.estado(id),
	CONSTRAINT fk_cliente_persona FOREIGN KEY (id_persona_pk) REFERENCES public.persona(id)
);

-- Permissions

ALTER TABLE public.cliente OWNER TO postgres;
GRANT ALL ON TABLE public.cliente TO postgres;


-- public.cuenta definition

-- Drop table

-- DROP TABLE public.cuenta;

CREATE TABLE public.cuenta (
	id int8 GENERATED ALWAYS AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 9223372036854775807 START 1 CACHE 1 NO CYCLE) NOT NULL,
	numerocuenta numeric NULL,
	id_cliente_pk int8 NULL,
	saldo varchar NULL,
	id_estado_pk int8 NULL,
	id_tipo_cuenta_pk int8 NULL,
	CONSTRAINT cuentas_pk PRIMARY KEY (id),
	CONSTRAINT unique_numero_cuenta UNIQUE (numerocuenta),
	CONSTRAINT fk_cuenta_cliente FOREIGN KEY (id_cliente_pk) REFERENCES public.cliente(id),
	CONSTRAINT fk_cuenta_estado FOREIGN KEY (id_estado_pk) REFERENCES public.estado(id),
	CONSTRAINT fk_cuenta_tipo FOREIGN KEY (id_tipo_cuenta_pk) REFERENCES public.tipo_cuenta(id)
);

-- Permissions

ALTER TABLE public.cuenta OWNER TO postgres;
GRANT ALL ON TABLE public.cuenta TO postgres;


-- public.movimiento definition

-- Drop table

-- DROP TABLE public.movimiento;

CREATE TABLE public.movimiento (
	id int8 GENERATED ALWAYS AS IDENTITY( INCREMENT BY 1 MINVALUE 1 MAXVALUE 9223372036854775807 START 1 CACHE 1 NO CYCLE) NOT NULL,
	id_cuenta_pk int8 NULL,
	fecha timestamp NULL,
	id_tipomovimiento_pk int8 NULL,
	valormovimiento numeric NULL,
	CONSTRAINT movimientos_pk PRIMARY KEY (id),
	CONSTRAINT fk_movimiento_cuenta FOREIGN KEY (id_cuenta_pk) REFERENCES public.cuenta(id),
	CONSTRAINT fk_movimiento_tipo FOREIGN KEY (id_tipomovimiento_pk) REFERENCES public.tipo_movimiento(id)
);

-- Permissions

ALTER TABLE public.movimiento OWNER TO postgres;
GRANT ALL ON TABLE public.movimiento TO postgres;


-- Permissions

GRANT ALL ON SCHEMA public TO postgres;
GRANT ALL ON SCHEMA public TO public;

```
