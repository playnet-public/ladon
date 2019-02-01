
# Database structure

##### Policies
```sql
CREATE TABLE IF NOT EXISTS policies (
    id serial primary key,
    description text NOT NULL DEFAULT '',
    effect bool NOT NULL DEFAULT false,
    metadata text NOT NULL DEFAULT
    createdAt timestamp with time zone NOT NULL DEFAULT NOW(),
    UNIQUE(id)
);
CREATE UNIQUE INDEX IF NOT EXISTS policies_idx_id ON policies (id);
```

##### Policy Subjects
```sql
CREATE TABLE IF NOT EXISTS policy_subjects (
    policyId integer references policies (id),
    subject text NOT NULL DEFAULT '',
    createdAt timestamp with time zone NOT NULL DEFAULT NOW(),
    UNIQUE(policyId, subject)
);
CREATE INDEX IF NOT EXISTS policy_subjects_idx_subject ON policy_subjects (subject);
```

##### Policy Resources
```sql
CREATE TABLE IF NOT EXISTS policy_resources (
    policyId integer references policies (id),
    resource text NOT NULL DEFAULT '',
    createdAt timestamp with time zone NOT NULL DEFAULT NOW(),
    UNIQUE(policyId, resource)
);
CREATE INDEX IF NOT EXISTS policy_resources_idx_resource ON policy_resources (resource);
```

##### Policy Actions
```sql
CREATE TABLE IF NOT EXISTS policy_actions (
    policyId integer references policies (id),
    action text NOT NULL DEFAULT '',
    createdAt timestamp with time zone NOT NULL DEFAULT NOW(),
    UNIQUE(policyId, action)
);
CREATE INDEX IF NOT EXISTS policy_actions_idx_action ON policy_actions (action);
```

##### Policy Conditions
```sql
CREATE TABLE IF NOT EXISTS policy_conditions (
    policyId integer references policies (id),
    name text NOT NULL DEFAULT '',
    options json NOT NULL DEFAULT '{}'::json,
    createdAt timestamp with time zone NOT NULL DEFAULT NOW(),
    UNIQUE(policyId, name)
);
CREATE INDEX IF NOT EXISTS policy_conditions_idx_name ON policy_conditions (name);
```
