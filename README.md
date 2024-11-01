# Texas-DPS-Scheduler
Book Texas DPS Appointments (fixes auth errors) 🚦

## Why?
DPS appointments are pretty much impossible to get and the website is a mess. This script automates the process of booking an appointment. Also, earlier versions of the script were broken due to authentication changes in the DPS website. This version fixes those issues. 

## Usage

1. Clone the repository
2. Copy `config.example.yaml` to `config.yaml` and fill in the required fields
3. Optionally setup notifications through [Apprise](https://github.com/caronc/apprise) by adding handlers in `monitor.py`
4. Run the following commands

```script
pip install requirements.txt
bash run.sh
```

Tip: You need to keep the script running in order to get an appointment. You can use GitHub Codespaces or a VPS to keep the script running 24/7.

> [!IMPORTANT]  
> There are occasional errors with authentication and selenium (about once per hour based on my experience), but they're expected. It's difficult to bypass the new authentication system every time, but it works out most times. Since monitor.py triggers the main script each minute, this ends up working to our advantage. Check out [#1](https://github.com/Syzygianinfern0/Texas-DPS-Scheduler/issues/1) for more details.
> There also seems to be an IP blocking issue when the script is run for too long. I would recommend starting the script the night before you want to book the appointment.

## Project Structure

- `config.example.yaml`: Example configuration file which needs to be copied to `config.yaml`
- `fingerprints.py`: Generates the auth fingerprint for the DPS website
- `main.py`: Main script that checks, holds, and books the appointment
- `monitor.py`: Calls main script periodically and sends notifications
- `run.sh`: Bash script to call the monitor script
