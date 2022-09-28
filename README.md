This is an [Ansible](http://www.ansible.com/home) role for installing Celery's Web UI [Flower](http://flower.readthedocs.io/en/latest/).

# What it Does

This role installs the `flower` Python module (using `pip`), defines
a `flower` service and a flowerconfig.py file and starts this service.

# Usage

A very basic playbook could look like this:

```yaml
- hosts: all
  roles:
    - role: flower
      vars:
        flower_port: 80
        flower_app_name: proj
        flower_app_dir: /my/cool/app
        flower_broker_url: http://localhost:5671
```

This role installs `celery`, however if you want to use your own celery installation, you can set the `{{ flower_venv_dir }}` variable without the /bin/celery part.  
For using apps with `flower`, it is important to set the `{{ flower_app_dir }}` variable to the app directory, which will be also the service working directory. The `{{ flower_app_name }}` is only the module name.  
When using this role for Galaxy servers, please set both:

- `{{ flower_app_dir }}`
- `{{ flower_python_path }}` (can be relative to app dir)

It is highly recommended to store `{{ flower_ui_users }}` and broker url/api vars in `secret_group_vars`.
