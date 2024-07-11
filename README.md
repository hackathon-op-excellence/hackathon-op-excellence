# PoC setup steps:

## run postgres container
docker run -p 5432:5432 --name some-postgres -e POSTGRES_PASSWORD=<password placeholder> -d postgres

(remember the password, you'll need to provide it in .env file)

## create mock data with psql

CREATE DATABASE jobboard;
\c jobboard
CREATE TABLE job_data (
    job_id SERIAL PRIMARY KEY,
    title VARCHAR(255),
    applications INT,
    location VARCHAR(255),
    posted_date DATE
);

INSERT INTO job_data (title, applications, location, posted_date) VALUES
('Software Engineer', 120, 'New York', '2023-07-01'),
('Data Analyst', 80, 'San Francisco', '2023-06-24'),
('Product Manager', 200, 'Remote', '2023-07-03');

## create venv
python -m venv new-env
source new-env/bin/activate  # On Windows use `new-env\Scripts\activate`

## install dependencies
launch from project's root the following command:

pip install -r requirements.txt

create .env file in the project root and fill it with:
OPENAI_API_KEY=
DB_NAME=jobboard
DB_USER=postgres
DB_PASSWORD=(password you used to run docker container)
DB_HOST=localhost
DB_PORT=5432
