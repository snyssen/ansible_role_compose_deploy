snyssen.compose_deploy
=========

This very simple role helps with deploying `docker-compose.yml` files and managing the state of the software stacks defined in them.

The `docker-compose.yml` file (and optionally its accompanying `.env` file) should be located in the usual templates folder under the filenames `docker-compose.yml` and `.env.j2` respectively.

Requirements
------------

See the [community.docker.docker_compose module requirements](https://docs.ansible.com/ansible/latest/collections/community/docker/docker_compose_module.html#requirements).

Role Variables
--------------

| Variable                 | Description                                                                                                                                                                                                                                                   | Default value                                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| stack_name           | The name of the container stack; used to build the `docker_compose_path` using its default value.                                                                                                                                                                                                     | `unspecified`                                         |
| docker_compose_directory | Directory which should hold the compose directories.                                                                                                                                                                                                          | `{{ ansible_user_dir }}/containers`                   |
| docker_compose_path      | The complete path to the directory that should hold the deployed `docker-compose.yml` file.                                                                                                                                                                   | `{{ docker_compose_directory }}/{{ stack_name }}` |
| deploy_env_template      | Whether the role should also look for a `.env.j2` template that should be deployed alongside the `docker-compose.yml` file.                                                                                                                                   | `false`                                               |
| docker_compose_state     | The state in which the stack should be after deployment. See the [community.docker.docker_compose module documentation](https://docs.ansible.com/ansible/latest/collections/community/docker/docker_compose_module.html#parameter-state) for possible values. | `present`                                             |

Dependencies
------------

None

Example Playbook
----------------

The following will fetch the first `docker-compose.yml` template file it sees (usually in the closest `templates` directory, according to Ansible rules), and deploy it under `/home/$USER/containers/my-container-stack/docker-compose.yml` (after running it through the Ansible templating engine). Finally, it will then run it (`docker compose up -d`).

```yml
- hosts: all
  roles:
    - name: snyssen.container_deploy
      vars:
        stack_name: my-container-stack
```

License
-------

GPL-3.0

Author Information
------------------

email: [dev@snyssen.be](mailto:dev@snyssen.be)
website: [snyssen.be](https://snyssen.be)
