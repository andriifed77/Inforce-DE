INSTRUCTIONS ON HOW TO BUILD AND RUN THE DOCKER CONTAINERS
   1. You need to download Docker Desktop. 
   You can follow this link to do this: https://www.enterprisedb.com/downloads/postgres-postgresql-downloads .
   2. You need to run Docker Desktop. Computer will restart and after another running of it.
   3. After that open any text editor and create file with requirements.txt name and paste it inside this file: 
   "pandas==1.3.3
   numpy==1.21.2
   psycopg2-binary==2.9.1"
   4. Create a file named '"Dockerfile"'(with quotes) in the root directory of the project without any extension. Fill it with this text: "FROM python:3.9-slim
   ENV PYTHONUNBUFFERED=1
   WORKDIR /app
   COPY requirements.txt /app/
   RUN pip install --no-cache-dir -r requirements.txt
   COPY . /app/
   CMD ["python", "your_script.py"]"
   5. Then open terminal and write "cd" and root directory. When it has been opened, write "docker build -t my_python_app ." 
   6. Docker containers should be successfully ran.

ASSUMPTIONS
   1. It is assumed that the PostgreSQL database schema includes the users and transactions tables with the specified columns. The users table should have columns for id, username, email, and created_at, while the transactions table should include id, user_id, amount, and transaction_date.
   2. The ETL process assumes that the data in the source database is consistent. This means there should be no orphaned records (e.g., transactions without corresponding users) and that data relationships are correctly maintained.
   3. The database is assumed to use UTC for all timestamps. Any necessary time zone conversions are managed by the application or ETL script.
   4. Basic error handling is assumed in the ETL script. It is expected that the script will handle standard issues such as connection problems or missing data gracefully.

VERIFICATION
   1. After running the ETL process, verify that the transformed data appears as expected in the PostgreSQL database. Check the relevant tables and ensure the data matches the transformations specified in the ETL script.
   2. Cross-check the results with expected outcomes. For example, if the ETL script aggregates transaction amounts by user, verify that the summed amounts are correct for a few sample users.
   3. Examine logs from the ETL process for any errors or warnings. Ensure that there are no unexpected issues reported during the execution.
   4. Perform consistency checks to ensure that there are no orphaned records or inconsistencies in the database. For example, ensure that all transactions have corresponding users in the users table.
