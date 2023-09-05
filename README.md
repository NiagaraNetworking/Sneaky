# Sneaky
Sneaky -- Enumerate a webserver for subdirectories with a dictionary file. Bash Script

echo ┏━━━┓╋╋╋╋╋╋╋╋┏┓
echo ┃┏━┓┃╋╋╋╋╋╋╋╋┃┃
echo ┃┗━━┳━┓┏━━┳━━┫┃┏┳┓╋┏┓
echo ┗━━┓┃┏┓┫┃━┫┏┓┃┗┛┫┃╋┃┃
echo ┃┗━┛┃┃┃┃┃━┫┏┓┃┏┓┫┗━┛┃
echo ┗━━━┻┛┗┻━━┻┛┗┻┛┗┻━┓┏┛
echo ╋╋╋╋╋╋╋╋╋╋╋╋╋╋╋╋┏━┛┃
echo ╋╋╋╋╋╋╋╋╋╋╋╋╋╋╋╋┗━━┛ by Russell Rockefeller NiagaraFallsNetworking.com
echo For Educational Purposes Only

#!/bin/bash

echo "Welcome to Sneaky - the Domain Subdirectory Checker Script!"

# Prompt the user for the domain to check
read -p "Please enter the domain to check (e.g., example.com): " domain

# Validate the user-supplied domain
if [ -z "$domain" ]; then
  echo "Error: Domain cannot be empty."
  exit 1
fi

# Prompt the user for the input file containing subdirectories
read -p "Please enter the path to the text file with subdirectories: " subdirs_file

# Check if the input file exists
if [ ! -f "$subdirs_file" ]; then
  echo "Error: The specified input file does not exist."
  exit 1
fi

# Prompt the user for the output file for results
read -p "Please enter the path to the results file: " results_file

# Initialize the results file
> "$results_file"

# Start processing the subdirectories
while read -r subdir; do
  # Use wget to check if the subdirectory exists
  wget -q --spider "$domain/$subdir"
  
  # Check the exit status of wget
  if [ $? -eq 0 ]; then
    echo "$domain/$subdir - Subdirectory exists" >> "$results_file"
  fi
  
  # Pause for 90 seconds
  sleep 90
done < "$subdirs_file"

echo "Done! Results have been saved to $results_file"

