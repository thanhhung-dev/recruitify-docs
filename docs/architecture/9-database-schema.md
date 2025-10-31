# 9. Database Schema

### PostgreSQL Database Schema

```sql
-- Users table for authentication and role management
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    role VARCHAR(50) NOT NULL CHECK (role IN ('JOB_SEEKER', 'RECRUITER')),
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- Profiles for JOB_SEEKER users
CREATE TABLE user_profiles (
    user_id UUID PRIMARY KEY REFERENCES users(id) ON DELETE CASCADE,
    first_name VARCHAR(255),
    last_name VARCHAR(255),
    headline TEXT,
    summary TEXT,
    avatar_url VARCHAR(255)
);

-- Work experiences linked to a user profile
CREATE TABLE work_experiences (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_profile_id UUID NOT NULL REFERENCES user_profiles(user_id) ON DELETE CASCADE,
    job_title VARCHAR(255) NOT NULL,
    company_name VARCHAR(255) NOT NULL,
    location VARCHAR(255),
    start_date DATE NOT NULL,
    end_date DATE, -- Can be NULL for current job
    description TEXT
);

-- Education history linked to a user profile
CREATE TABLE education (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_profile_id UUID NOT NULL REFERENCES user_profiles(user_id) ON DELETE CASCADE,
    school_name VARCHAR(255) NOT NULL,
    degree VARCHAR(255),
    field_of_study VARCHAR(255),
    start_date DATE NOT NULL,
    end_date DATE
);

-- Centralized skills table to prevent duplicates
CREATE TABLE skills (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(100) UNIQUE NOT NULL
);

-- Join table to create a many-to-many relationship between profiles and skills
CREATE TABLE user_profile_skills (
    user_profile_id UUID NOT NULL REFERENCES user_profiles(user_id) ON DELETE CASCADE,
    skill_id UUID NOT NULL REFERENCES skills(id) ON DELETE CASCADE,
    PRIMARY KEY (user_profile_id, skill_id)
);

-- Create indexes on foreign keys for faster queries
CREATE INDEX ON work_experiences (user_profile_id);
CREATE INDEX ON education (user_profile_id);
CREATE INDEX ON user_profile_skills (user_profile_id);
CREATE INDEX ON user_profile_skills (skill_id);
```

---
