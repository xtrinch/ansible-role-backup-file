Role Name
=========

Create entry in user crontab for backuping a file defined with role variables `directory` and `filename` to directory defined with `backup_directory`, and deleting entries older than 7 days

Role Variables
--------------

Should be overridden:

    directory: "/home/{{ ansible_ssh_user}}"
    filename: "backMeUp.test"
    backup_directory: "/home/{{ansible_ssh_user}}/backups"
    
Only override if necessary:

    cronjob_backup: '*/5 * * * * cp {{ directory }}/{{ filename }} {{ backup_directory }}/{{ filename }}`date +\%d\%m\%y\%H\%M`.bak > /dev/null'
    cronjob_delete_old: '*/5 * * * * find /home/{{ ansible_ssh_user }}/backups -mtime +7 -exec rm -f {} \;'

Dependencies
------------


Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: xtrinch.kiosk, 
                directory: "/home/{{ ansible_ssh_user}}",
                filename: "backMeUp.test",
                backup_directory: "/home/{{ansible_ssh_user}}/backups" }

License
-------

BSD

