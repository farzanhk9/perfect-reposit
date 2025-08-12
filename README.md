import os
import subprocess
import random
import datetime

# Professional commit messages
messages = [
    "Code formatted using Black 🖤",
    "Applied automatic code formatting",
    "Improved code readability",
    "Consistent style applied",
    "Formatted Python files for better clarity",
    "Code style updated for consistency",
    "Minor formatting improvements",
    "Applied PEP 8 formatting standards"
]

def run_command(command):
    """Run a shell command and print output."""
    result = subprocess.run(command, shell=True, capture_output=True, text=True)
    if result.stdout:
        print(result.stdout)
    if result.stderr:
        print(result.stderr)

# Step 1: Install Black if not available
print("📦 Checking for Black formatter...")
run_command("pip install black --quiet")

# Step 2: Format all Python files in the repo
print("🎨 Formatting Python files...")
run_command("black .")

# Step 3: Pick random commit message
msg = random.choice(messages)

# Step 4: Commit and push changes
print(f"💾 Committing with message: {msg}")
run_command("git add .")
run_command(f'git commit -m "{msg}"')
run_command("git push")

# Step 5: Log the action
with open("format_log.txt", "a", encoding="utf-8") as f:
    f.write(f"{datetime.datetime.now()}: {msg}\n")

print("✅ All done! Your code is clean and committed.")
