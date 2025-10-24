# DEPLOYMENT PROCESS + DOCUMENTATION

1.  Everything starts with VPS on Hetzner

    - every process/app/API/website needs to live somewhere click on create/add server
    ![create](./assets/hetzner/hz-create.jpeg){ loading=lazy }

2.  Configure server specs depending on needs
    ![create](./assets/hetzner/hz-create-pricing.jpeg){ loading=lazy }
    - \[create table / guide for pricing]
    - By default to cheapest option (Most of the time this is providing good enough anyways)
      ![pricing](./assets/hetzner/hz-create-pricing-select.jpeg){ loading=lazy }
    - location on cheapest option doesn't matter, otherwise select US-east "Ashburn, VA"
      ![country](./assets/hetzner/hz-create-country.jpeg){ loading=lazy }
    - select image \[Ubuntu 24.04] unless needed otherwise, this can be changed after
      ![so](./assets/hetzner/hz-create-so.jpeg){ loading=lazy }
    - networking leave default, unless making APIs, this can be changed after
      ![network](./assets/hetzner/hz-create-network.jpeg){ loading=lazy }
    - SSH keys (you should have some created) select the ones you will need, can also be changed after
      ![ssh](./assets/hetzner/hz-create-ssh.jpeg){ loading=lazy }
      - if you don't select any, it will email you root credentials
        ![credentials](./assets/hetzner/hz-create-credentials.jpeg){ loading=lazy }

    - leave remaining fields empty (default) unless needed
    - volumes → need to add additional storage?
    - firewalls → restrict traffic
    - backups → daily copy of server disk
    - placement groups → optimize availability
    - labels → organization?
    - cloud config → execute custom server scripts
    - rename server for project
    - lowercase name of business or project
    - use '-' dashes for spaces
    - do not use numbers or symbols
    - add at the end a descriptor if necessary
    - duosis-website-test
    - saras-cocina-migration
      ![dashboard](./assets/hetzner/hz-create-dashboard.jpeg){ loading=lazy }
3.  Add server to coolify
    ![ssh](./assets/hetzner/co-add.jpeg){ loading=lazy }
    - use same name as Hetzner server
    - add simple description
    - add the IP address of the server itself \!\!\!
    - change ssh key to coolify key
      ![ssh](./assets/hetzner/co-rename.jpeg){ loading=lazy }
4.  Validate and set-up docker on server
    - if first time set-up, coolify will automatically download and install docker on server
      ![ssh](./assets/hetzner/co-validate-docker.png){ loading=lazy }

**END THATS A COMPLETE SERVER SETUP\! NOW DEPLOYMENT... →**

---

5.  ## Create a Project in coolify
    ![ssh](./assets/hetzner/co-project-add.png){ loading=lazy }
    - to add a name → help serve as server for consistency
    - to add a description of project
      ![ssh](./assets/hetzner/co-project-add-name.png){ loading=lazy }

6.  ## Create DEV environment
    - by default a project will come with "production" environment, the dev environment must be added manually
    - optional: more environments can be created here. For example: TEST, STAGE, etc.
      ![ssh](./assets/hetzner/co-environment.png){ loading=lazy }

7.  ## Create resources for each environment, starting with DEV
    - there are many different ways to create resources in coolify
      ![ssh](./assets/hetzner/co-resource.png){ loading=lazy }
    - most likely you are working/deploying from a private GH repo (github)
      ![ssh](./assets/hetzner/co-resource-options.png){ loading=lazy }
      ![ssh](./assets/hetzner/co-resource-options-select.png){ loading=lazy }
    - select the server it belongs to
      ![ssh](./assets/hetzner/co-resource-options-server.png){ loading=lazy }
    - select the github-app to use
      ![ssh](./assets/hetzner/co-select-githubapp.png){ loading=lazy }
    - select the repo and load it
      ![ssh](./assets/hetzner/co-select-repo.png){ loading=lazy }
    - select branch → first with "dev" branch and later in prod env. with "main"
    - change build pack to docker compose
    - change location of base docker-compose.yml file
    - **NOTE\!\!** `.yml` and `.yaml` are different ensure correct one is set
      ![ssh](./assets/hetzner/co-select-repo-branch.png){ loading=lazy }

8.  ## Configure resources + deployment (application)
    ![ssh](./assets/hetzner/co-configuration.png){ loading=lazy }
    - name the application → maintain format `<app-name-dev>` for dev env. and `<app-name-prod>` for prod
    - add description
    - Domains will need its own exec
    - if no domains are purchased or configured yet, generate new domain
    - if configured, use "https://www.google.com/search?q=dev.domain-name.com" for dev and "[www.domain-name.com](https://www.google.com/search?q=https://www.domain-name.com)" for prod.
    - add custom build or start commands if necessary
    - add environment variables
    - use developer view to add/edit in bulk
    
9.  ## Deploy and test\!
    - hit first deploy button and hope for the best. → If everything is on docker, it should work
    - it is more likely a config error.

---

**Author:** Wesley Ordonez  
**Last updated:** October 23, 2025
