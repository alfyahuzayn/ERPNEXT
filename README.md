# Biometric Attendance Sync Tool for ERPNext v15

This guide provides step-by-step instructions on integrating biometric attendance devices with ERPNext version 15 using the Frappe Biometric Attendance Sync Tool. Follow these steps to set up the synchronization for accurate attendance tracking.

## Prerequisites:

- ERPNext v15 installed.
- Biometric attendance devices with device IDs/RFIDs mapped to employees.

## Step 1: Define Employee Shift Details

1. Set up employees and their shifts in ERPNext to enable the Auto Attendance feature.

## Step 2: Map Employees to Attendance Devices

1. Navigate to `Employee > Attendance and Leave Details > Attendance Device ID`.
2. Enter the Biometric or RF tag ID for each employee.

## Step 3: Define Shift Details in ERPNext

1. Search for and open the "Employee Check In" DocType.
2. Add Shift Details:
    - In the "Fields" section, add fields for shift type, shift timings, or any other relevant details.
    - Save the changes.

## Step 4: Integrating Frappe HR with Biometric Attendance Devices

### Step 4.1: API Integration

1. Open a terminal and navigate to `frappe-bench > apps > frappe > frappe > biometric-attendance-sync-tool`.
2. Activate the virtual environment with the command: `source ~/frappe-bench/env/bin/activate`.
3. Install the required dependencies: `pip install -r requirements.txt`.

### Step 4.2: Configure the Sync Tool

- Rename `local.config.py.template` to `local.config.py`.
- Edit `local.config.py` and configure the following parameters:

    ```python
    ERPNEXT_API_KEY = 'your_api_key'
    ERPNEXT_API_SECRET = 'your_api_secret'
    ERPNEXT_URL = 'http://your_erpnext_url:8000'
    ERPNEXT_VERSION = 15

    devices = [{'device_id': 'test_1', 'ip': 'device_ip_address', 'punch_direction': 'AUTO', 'clear_from_device_on_fetch': False}]
    # Add more devices if needed

    shift_type_device_mapping = [{'shift_type_name': ['your_shift_type'], 'related_device_id': ['test_1']}]
    # Map shift types to device IDs
    ```

## Step 5: Run the Sync Tool

- Execute the sync tool with the command: `python3 erpnext_sync.py`.
- This will fetch the data from the configured biometric devices and synchronize it with ERPNext.

## Additional Notes

- Ensure that you have generated API Key and Secret Key for the ERPNext administrator.
- Update device details and shift mappings in the `local.config.py` file.
- If you encounter any issues or have questions, please check the [Frappe Biometric Attendance Sync Tool repository](https://github.com/frappe/biometric-attendance-sync-tool) for support.
- For community discussions and assistance, visit the [ERPNext Forum](https://discuss.erpnext.com/).
