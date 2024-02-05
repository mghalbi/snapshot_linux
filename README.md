# Snapshot Playbooks

This set of Ansible playbooks is designed to capture, analyze, and compare the status of a machine's configuration. The playbooks are organized as follows:

## 1. `snapshot.yml`

This playbook is responsible for creating a snapshot of the machine's status. It performs the following tasks:

- Gathers facts about the system, including services, mounts, users, and TCP ports.
- Retrieves information about crontab entries, environment variables, aliases, and running processes for each user.
- Generates a timestamped snapshot YAML file containing the collected information.

## 2. `get_status.yml`

This playbook is imported by `snapshot.yml` and is responsible for obtaining detailed information about services, crontab, environment variables, aliases, and mounts.

## 3. `audit.yml`

This playbook checks the consistency of the machine's current state with a previously captured snapshot. It verifies the following:

- Checks if the specified snapshot folder exists.
- Finds all YAML files in the folder.
- Retrieves the content of the latest snapshot file.
- Compares the current machine state with the captured snapshot.
- Prints out the differences (delta) for services, ports, mounts, crontab, environment variables, and aliases.

## Usage

1. Ensure that Ansible is installed on the local machine.
2. Edit the `vars.yml` file to configure variables such as `snapshot_path`, `user`, and `group`.
3. Run the playbooks using the following commands:

   ```bash
   ansible-playbook snapshot.yml
   ansible-playbook audit.yml
   ```
