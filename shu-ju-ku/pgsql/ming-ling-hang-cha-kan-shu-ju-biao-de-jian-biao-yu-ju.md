# 命令行查看数据表的建表语句

```text
pg_dump -U hjg -d devops_dev -W -s -t sc_aws_ec2_info -h 192.168.31.23

 -W, --password 
 -s, --schema-only 
 -t, --table=TABLE   

####显示结果
--
-- PostgreSQL database dump
--

-- Dumped from database version 9.5.19
-- Dumped by pg_dump version 10.10 (Ubuntu 10.10-0ubuntu0.18.04.1)

SET statement_timeout = 0;
SET lock_timeout = 0;
SET idle_in_transaction_session_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;

SET default_tablespace = '';

SET default_with_oids = false;

--
-- Name: sc_aws_ec2_info; Type: TABLE; Schema: public; Owner: hjg
--

CREATE TABLE public.sc_aws_ec2_info (
    id integer NOT NULL,
    name_tag text,
    public_ip text,
    private_ip text,
    key_tag text,
    mac_addr text,
    public_dns_name text,
    create_at timestamp without time zone DEFAULT now(),
    update_at timestamp without time zone DEFAULT now(),
    instance_type text,
    instance_owner text,
    instance_id text
);


ALTER TABLE public.sc_aws_ec2_info OWNER TO hjg;


```

与在dg工具显示出来的ddl是一样的

```text
-- auto-generated definition
create table sc_aws_ec2_info
(
    id              serial not null,
    name_tag        text,
    public_ip       text,
    private_ip      text,
    key_tag         text,
    mac_addr        text,
    public_dns_name text,
    create_at       timestamp default now(),
    update_at       timestamp default now(),
    instance_type   text,
    instance_owner  text,
    instance_id     text
);

alter table sc_aws_ec2_info
    owner to hjg;

```

