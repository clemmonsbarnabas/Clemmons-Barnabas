# Clemmons-Barnabas
# Step 1: Use an official Python runtime as the base image (or any app-specific base image)
FROM python:3.11-slim

# Step 2: Install cowsay and any required dependencies
RUN apt-get update && apt-get install -y \
    fortune-mod \
    cowsay \
    && rm -rf /var/lib/apt/lists/*

# Step 3: Install any application dependencies (e.g., Flask or others)
WORKDIR /app
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

# Step 4: Copy the rest of the application files
COPY . /app/

# Step 5: Set up a fun "cowsay" script (You could modify this for your actual Wisecow app)
COPY run_cow_script.sh /app/run_cow_script.sh
RUN chmod +x /app/run_cow_script.sh

# Step 6: Expose the port your app will use (e.g., 5000 for Flask)
EXPOSE 5000

# Step 7: Start the app (or run a fun cowsay script)
CMD ["/app/run_cow_script.sh"]
