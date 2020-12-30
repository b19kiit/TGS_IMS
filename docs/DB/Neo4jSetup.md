# Setup Graph DB

## Local Development

- Install Neo4j Desktop Enterprise Version.

- SignIn to neo4j account

- Create a New Project

- Open the project window & Create new Database

> - Create database with {name:"IMS", Password:<>, version:"4.1.3" or higher}

- Disable required Firewalls

- Add unique index to `User.user_id`

```cypher
CREATE CONSTRAINT unique_user_id
ON (u:User) ASSERT u.user_id IS UNIQUE
```
