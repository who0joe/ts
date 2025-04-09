### Cron Job Test: Execute Every Second

#### Test Setup

1. Create a script `test_script.sh` that logs the current timestamp to a file every second:
    ```bash
    #!/bin/bash
    while true; do
        echo "Log entry at $(date)" >> /tmp/test_cron.log
        sleep 1
    done
    ```

2. Make the script executable:
    ```bash
    chmod +x test_script.sh
    ```

3. Add the following cron job to execute the script:
    ```bash
    @reboot /path/to/test_script.sh
    ```

#### Test Steps

1. Reboot the system to start the cron job.
2. Verify that the script is running:
    ```bash
    ps aux | grep test_script.sh
    ```

3. Check the log file `/tmp/test_cron.log` to ensure entries are being added every second:
    ```bash
    tail -f /tmp/test_cron.log
    ```

#### Expected Output

- The log file `/tmp/test_cron.log` should contain entries with timestamps incrementing every second.

#### Cleanup

1. Stop the script:
    ```bash
    pkill -f test_script.sh
    ```

2. Remove the log file:
    ```bash
    rm /tmp/test_cron.log
    ```

3. Remove the cron job:
    ```bash
    crontab -e
    # Delete the line with @reboot /path/to/test_script.sh
    ```