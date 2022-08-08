# Prisma

## Setup

### Dependencies
```
npm i --save-dev prisma typescript ts-node @types/node nodemon
```
* Typescript because prisma is built in top of typescript
* ts-node and @types/node for node

<hr/>

## Initialize prisma
```
npx prisma init --datasource-provider postgresql
```
This will initialize prisma for postgres and create basic files.

<hr/>

## Format primsa file
You can either install the vs code extension or run `npx prisma format`

<hr/>

## schema.prisma file

- **generator** - what your prisma file will be generating into. Default is `prisma-client-js`.
- **provider** - where data is coming from i.e. postgresql, mysql, mongodb.
- **url** - database url which is defined in env variable.

<hr/>

## Basic Prisma Model Setup

```
model User {
  id   Int    @id @default(autoincrement())
  name String
}
```

<hr/>

##  Prisma Migration Basics

Prisma and database are separated from one another. We need to run schema.prisma file to migrate changes.

```
npx prisma migrate dev --name init
```
dev here means for development only and name is for name of migration.
This will also create prisma client that we put in schema.prisma file. Every time you make migration, it will update the prisma client. Prisma client is all the code for interacting with the database. 

### Installing client 
```npm i @prisma/client```

Migration will automatically generate the client but if you want to manually generate the client, run:
`npx prisma generate`

<hr/>

## Datasources and Generators

- Only one datasource because only one database
- Datasource must have provider and url
- You can have multiple generators. For e.g. for prima client, for graphql api

<hr/>

## Model Fields

- Model represents different tables inside your database and each modal is composed of different fields.
- Field is composed of 4 different parts.
  * 1st field is name of field (required)
  * 2nd field is type of field (required)
  * 3rd field is attribute (optional)
  * 4th field is attribute (optional)

There is also field modifier.

### Fields
- Int 
- String 
- Boolean 
- BigInt 
- Float (less specific) 
- Decimal (for large numbers like BigInt) 
- DateTime
- Json (only for supported database like Postgres but not for  sqlite)
- Bytes (for big data like file data)
- Unsupported (you will not write this data type yourself, but prisma will use this data type if it finds upsupported type if you migrate your exisitng data type)


### Field modifier
There are two types of field modifiers: 
- [] : Post[] There could be multiple of post
- ? : String? This represents the field is optional


### Attributes
- @id
- @relation
- @unique
- @updatedAt
- @default(now()) 

### Field level attribute vs Blocal level attribute
**Field level attribute** applies to the field
**Block level attribute** applies to the model (table)
