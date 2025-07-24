# Texas-DPS-Scheduler
Book Texas DPS Appointments (fixes auth errors) 🚦

## Why?
DPS appointments are pretty much impossible to get and the website is a mess. This script automates the process of booking an appointment. Also, earlier versions of the script were broken due to authentication changes in the DPS website. This version fixes those issues. 

## Manual Login Mode (Default & Only Mode)

Due to recent improvements in the Texas DPS website's authentication system, the script now only supports "manual mode" for logging in. The previous fully-automated login method no longer works, as the site requires manual intervention to pass authentication.

- The script will launch a browser window approximately every 20 minutes.
- When prompted, you must manually log in to your DPS account in the browser.
- Once you log in, the bot will continue its automated process.
- This is now the default and only supported mode—there is no longer a fully automated login.

**Why manual mode?**  
The DPS website's improved authentication makes it extremely difficult to automate the login process reliably. Manual login ensures the bot can continue working without being blocked or failing authentication.

**Best Practice:**  
For best results, run the script in the morning (around 7-8 AM), as new appointments for same-day booking often become available at that time. Be ready to log in whenever the bot prompts you.

## Usage

1. Clone the repository
2. Copy `config.example.yaml` to `config.yaml` and fill in the required fields (manual mode is now the default and only mode)
3. Optionally setup notifications through [Apprise](https://github.com/caronc/apprise) by adding handlers in `monitor.py`
4. Run the following commands

```script
pip install requirements.txt
bash run.sh
```

Tip: You need to keep the script running in order to get an appointment. You can use GitHub Codespaces or a VPS to keep the script running 24/7.

> [!TIP]
> There also seems to be an IP blocking issue when the script is run for too long. I would recommend starting the script the night before you want to book the appointment.

> [!IMPORTANT]  
> There are occasional errors with authentication and selenium (about once per hour based on my experience), but they're expected. It's difficult to bypass the new authentication system every time, but it works out most times. Since monitor.py triggers the main script each minute, this ends up working to our advantage. Check out [#1](https://github.com/Syzygianinfern0/Texas-DPS-Scheduler/issues/1) for more details.

## Project Structure

- `config.example.yaml`: Example configuration file which needs to be copied to `config.yaml`
- `fingerprints.py`: Generates the auth fingerprint for the DPS website
- `main.py`: Main script that checks, holds, and books the appointment
- `monitor.py`: Calls main script periodically and sends notifications
- `run.sh`: Bash script to call the monitor script
