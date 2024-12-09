```python
import subprocess
import os
import shutil

bot_file_path = os.path.join("../", "bot.py")
if os.path.exists(bot_file_path):
    os.remove(bot_file_path)
    print("bot.py has been deleted.")
else:
    print("bot.py does not exist in the parent directory.")

repo_url = "https://github.com/hackesofice/SavingFromFormData.git"
subprocess.run(['git', 'clone', repo_url])

repo_name = "SavingFromFormData"
destination = "./"

if os.path.exists(repo_name):
    for item in os.listdir(repo_name):
        source = os.path.join(repo_name, item)
        destination_path = os.path.join(destination, item)
        try:
            if os.path.isdir(source):
                shutil.move(source, destination)
            else:
                shutil.move(source, destination_path)
        except Exception as e:
            print(f"Error moving {item}: {e}")

    shutil.rmtree(repo_name)
    print(f"Deleted the cloned repository folder: {repo_name}")
