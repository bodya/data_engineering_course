```sql
CREATE TABLE segments
(
 segment_id int NOT NULL,
 segment    varchar(50) NOT NULL,
 CONSTRAINT PK_46 PRIMARY KEY ( segment_id )
);

CREATE TABLE shipping
(
 shipping_mode_id int NOT NULL,
 shiping_mode     varchar(50) NOT NULL,
 CONSTRAINT PK_36 PRIMARY KEY ( shipping_mode_id )
);

CREATE TABLE address
(
 geo_id      int NOT NULL,
 country     varchar(50) NOT NULL,
 region      varchar(50) NULL,
 "state"       varchar(50) NULL,
 city        varchar(50) NULL,
 postal_code int NULL,
 CONSTRAINT PK_28 PRIMARY KEY ( geo_id )
);

CREATE TABLE calendar
(
 order_date date NOT NULL,
 ship_date  date NOT NULL,
 year       int4range NULL,
 quarter    varchar(50) NULL,
 month      int4range NULL,
 week       int4range NULL,
 week_day   int4range NULL,
 day        int4range NULL,
 CONSTRAINT PK_5 PRIMARY KEY ( order_date, ship_date )
);

CREATE TABLE customers
(
 customer_id   varchar(50) NOT NULL,
 customer_name varchar(50) NOT NULL,
 CONSTRAINT PK_50 PRIMARY KEY ( customer_id )
);



CREATE TABLE products
(
 product_id   int NOT NULL,
 category     varchar(50) NULL,
 sub_category varchar(50) NULL,
 product_name varchar(150) NOT NULL,
 CONSTRAINT PK_40 PRIMARY KEY ( product_id )
);

CREATE TABLE sales
(
 row_id           int NOT NULL,
 order_id         varchar(50) NOT NULL,
 order_date       date NOT NULL,
 ship_date        date NOT NULL,
 shipping_mode_id int NOT NULL,
 segment_id       int NOT NULL,
 customer_id      varchar(50) NOT NULL,
 product_id       int NOT NULL,
 geo_id           int NOT NULL,
 sales            numeric(9,4) NULL,
 quantity         int NULL,
 discount         numeric(4,2) NULL,
 profit           numeric(9,4) NULL,
 reterned         varchar(5) NULL,
 CONSTRAINT PK_13 PRIMARY KEY ( row_id ),
 CONSTRAINT FK_22 FOREIGN KEY ( order_date, ship_date ) REFERENCES calendar ( order_date, ship_date ),
 CONSTRAINT FK_67 FOREIGN KEY ( product_id ) REFERENCES products ( product_id ),
 CONSTRAINT FK_70 FOREIGN KEY ( geo_id ) REFERENCES address ( geo_id ),
 CONSTRAINT FK_73 FOREIGN KEY ( customer_id ) REFERENCES customers ( customer_id ),
 CONSTRAINT FK_76 FOREIGN KEY ( segment_id ) REFERENCES segments ( segment_id ),
 CONSTRAINT FK_79 FOREIGN KEY ( shipping_mode_id ) REFERENCES shipping ( shipping_mode_id )
);

CREATE INDEX FK_24 ON sales
(
 order_date,
 ship_date
);

CREATE INDEX FK_69 ON sales
(
 product_id
);

CREATE INDEX FK_72 ON sales
(
 geo_id
);

CREATE INDEX FK_75 ON sales
(
 customer_id
);

CREATE INDEX FK_78 ON sales
(
 segment_id
);

CREATE INDEX FK_81 ON sales
(
 shipping_mode_id
);
```

